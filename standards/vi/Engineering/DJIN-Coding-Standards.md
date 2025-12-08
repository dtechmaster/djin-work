# DJIN Tech — Tiêu Chuẩn Mã Hóa

> Cấu trúc rõ ràng. Mô hình hàm. Đơn giản thông qua các hàm. Zod ở cốt lõi. Con người có thể đọc được.

---

## Phong Cách Mã

### Chỉ Composition API & TypeScript

* Sử dụng `<script setup lang="ts">`
* Không trộn lẫn Options API trừ khi có lý do chính đáng rõ ràng.

### Khai Báo Hàm

* ❌ Tránh các hàm ẩn danh: `const x = () => {}`
* ✅ Sử dụng các hàm có tên: `function x() {}`

### Khối #region

* Sử dụng `// #region` và `// #endregion` một cách nhất quán
* Hoạt động trong `.ts`, `.vue`, và các khối template

```vue
<template>
  <!--#region Feature A -->
  <div>{{ sayHello() }}</div>
  <!--#endregion Feature A -->
</template>

<script setup lang="ts">
//#region Imports
import nuxt from 'nuxt'
//#endregion

//#region Feature A
const greeting = 'Hello World!'
function say(str: string) { return str }
function sayHello() { return say(greeting) }
//#endregion
</script>
```

> 💡 VS Code: `[CTRL+K CTRL+8]` để thu gọn tất cả các vùng

### Sử Dụng Logger

* Tạo một composable lớp `Logger` để xử lý logging nếu chưa tồn tại
* Logger phải luôn có các phương thức `log`, `info`, `warn`, `error`
* Logs phải có thể đọc được như `[INFO][YYYY-MM-DD HH:MM:SS][File:Line] Message`
* Thay thế tất cả `console.log` bằng `Logger.log`

---

### Lập Trình Nullable

* Giả định tất cả các giá trị có thể là null hoặc undefined — đặc biệt là các giá trị lồng nhau
  → Không tin tưởng gì, thậm chí là mã của chính bạn.
* Sử dụng optional chaining (`?.`) một cách nhất quán để tránh lỗi runtime
  → `user?.profile?.address?.street`
* Cung cấp các giá trị dự phòng bằng cách sử dụng nullish coalescing (`??`) hoặc factories mặc định
  → `const name = user?.profile?.name ?? 'ゲスト'`
* Không bao giờ ném ngoại lệ trong UI — thay vào đó:

  * Sử dụng `v-if`, `v-else`, hoặc các component skeleton/loading
  * Vô hiệu hóa các nút hoặc input khi dữ liệu bị thiếu
  * Hiển thị các thông báo xác thực hoặc cảnh báo rõ ràng
* Ưu tiên các computed property phòng thủ hơn là lạc quan
  → Bọc trong các dự phòng an toàn hoặc các bảo vệ try/catch khi cần thiết
* Tránh tin tưởng sâu vào các kiểu, ngay cả trong TypeScript — cấu trúc vẫn có thể bị phá vỡ khi runtime (ví dụ: từ API hoặc localStorage)

---

## Mẫu Kiến Trúc

### Mô Hình Black Box

* Tránh trạng thái toàn cục hoặc các cấu trúc giống class trừ khi thực sự cần thiết
* Ưu tiên composition hơn logic dựa trên class
* Mọi thứ là một hàm, đối tượng, component, hoặc composable. Không kế thừa class
* Tránh trạng thái toàn cục hoặc các cấu trúc giống class trừ khi thực sự cần thiết

### Cấu Trúc Tiện Ích

Tổ chức logic mục đích chung vào `utils/`:

* `arrays.ts`
* `objects.ts`
* `japanese.ts`
* v.v.

Kiểm tra trước khi triển khai các tiện ích mới để tránh trùng lặp.

### Composables

Tránh quy ước `useX()`. Sử dụng các composable toàn cục có tiền tố `$`:

```ts
export default const $myComposable = {
  foo() {
    return 'bar'
  }
} as const
```

* Phải được khai báo như `const` được xuất mặc định
* Phải bắt đầu bằng `$`

---

## Zod như SST (Single Source of Truth)

### Nguyên Tắc

Zod định nghĩa mọi interface trong hệ thống:

* Xác thực
* Kiểu
* Props
* Logic dựa trên shape

### Loại Interface

| Loại     | Trường Hợp Sử Dụng                           | Ví Dụ                     |
|----------|----------------------------------------------|---------------------------|
| System   | Trang, component, composable                 | `z.system.pageSchema`     |
| Database | Cấu trúc PostgreSQL, xác thực, di chuyển     | `z.database.userSchema`   |

### Lợi Ích

* Trích xuất kiểu và props từ cùng một schema
* Nơi trung tâm cho logic nhất quán
* Loại bỏ sự trùng lặp interface
* Có thể xây dựng cấu trúc cơ sở dữ liệu từ các interface hệ thống và áp dụng triết lý của Steve Jobs (`"Bắt đầu phát triển từ quan điểm người dùng, sau đó chúng ta phát triển công nghệ"`)

Lưu trữ các schema được chia sẻ trong một thư mục có thể truy cập toàn cục và tái sử dụng chúng trên tất cả các lớp.

### Kích Thước Tệp

* Chúng ta nên giữ các tệp ngắn gọn, nhỏ và tập trung. Nếu một tệp quá lớn, nó nên được chia thành các tệp nhỏ hơn. `Lý tưởng`, mỗi tệp nên có một mục đích duy nhất và ít hơn 2000 dòng. `Lý tưởng`.

### Quy Ước Đặt Tên

* Sử dụng `I` cho interface, `T` cho kiểu và `P` cho props
* Sử dụng `camelCase` cho interface, kiểu và props
* Sử dụng `snake_case` cho các cột cơ sở dữ liệu, bảng và di chuyển
* Sử dụng `snake_case` cho biến môi trường và tệp cấu hình
* Sử dụng tiền tố `ENV_` cho biến môi trường và tiền tố `CONFIG_` cho tệp cấu hình

---

## Nguyên Tắc Thực Thi

> Luôn luôn lập kế hoạch trước khi mã hóa
> "Đầu tiên, giải quyết vấn đề. Sau đó, viết mã." — John Johnson
> "Lập trình viên tồi lo lắng về mã. Lập trình viên giỏi lo lắng về cấu trúc dữ liệu và mối quan hệ của chúng." — Linus Torvalds

## CLI

* Luôn sử dụng Deno cho CLI
* Sử dụng `npm specifiers` của Deno cho CLI để chúng ta có thể tránh các vấn đề quản lý phụ thuộc (https://deno.com/blog/not-using-npm-specifiers-doing-it-wrong)

## Kiểm Thử

* **Luôn viết kiểm thử** cho các công cụ CLI, tiện ích và chức năng cốt lõi khi chúng ngắn gọn và có ý nghĩa
* Kiểm thử nên đơn giản, tập trung và bao gồm các trường hợp sử dụng chính
* Sử dụng framework kiểm thử tích hợp của Deno với `Deno.test()`
* **Tổ Chức Kiểm Thử**:
  - Tạo thư mục `tests/` trong thư mục gốc dự án
  - Các tệp kiểm thử nên được đặt tên `*.test.ts` và đặt trong thư mục `tests/`
  - Phản ánh cấu trúc nguồn: `src/foo.ts` → `tests/foo.test.ts`
  - Đối với các dự án CLI, kiểm thử chính nằm trong `tests/main.test.ts`
* Tập trung vào kiểm thử:
  - Phân tích cú pháp và xác thực đối số CLI
  - Xử lý lỗi và các trường hợp biên
  - Tải biến môi trường
  - Các hàm logic kinh doanh cốt lõi
* Giữ kiểm thử có thể duy trì - nếu một kiểm thử trở nên phức tạp, hãy xem xét tái cấu trúc mã đang được kiểm thử
* Kiểm thử nên nhanh chóng và độc lập - không có phụ thuộc bên ngoài hoặc sửa đổi hệ thống tệp khi có thể

---

## Tài Nguyên Khác

* sử dụng `./DJIN-standards.md` để tham khảo
* sử dụng `./SYSTEM_SPECS.md` để tham khảo
* sử dụng `./EXECUTION_PLAN.md` để tham khảo
