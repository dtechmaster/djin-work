# ✔ PRINTABLE CHECKLIST — QA-ST-0001

**[← Back to Complete Standard](../../standards/en/QA/QA-ST-0001.md)**

---

### **BEFORE STARTING**

☐ Environment declared (in-house-preview / customer-preview / production)
☐ Credentials noted (ID + password)
☐ Display name verified (for name order tests)

---

## **1. Translations**

**If you are a native DJIN Member of the language:**
☐ Translations validated using native knowledge
☐ DeepL/Takoboto used as support in case of doubt

**If you are a non-native DJIN Member:**
☐ Complete texts validated in DeepL
☐ Individual words validated in Takoboto

**For everyone:**
☐ Name order according to UI language
☐ Avatar + Name displayed correctly

---

## **2. Spellcheck**

☐ No typos in UI
☐ No visible backend typos
☐ Translations x→JA checked in DeepL
☐ Individual words checked in Takoboto

---

## **3. Basic Data**

☐ No placeholders ("aaa", "test", lorem ipsum)
☐ Nothing offensive
☐ Appropriate fictional names (JP/BR)

---

## **4. Interface Translation**

☐ Buttons in correct language
☐ Nothing lost in pt-BR
☐ Nothing lost in English
☐ Name order ok

---

## **5. Leaks**

☐ No UUID showing
☐ No internal ID
☐ No stacktrace
☐ Nothing like undefined/null/[object Object]
☐ No raw API error
☐ No exposed technical messages

---

## **6. Layout**

Tests in:

* ☐ Desktop
* ☐ iPhone-width (~390px)

Check:
☐ Nothing overflows container
☐ No horizontal scroll
☐ Buttons click
☐ Lists load

---

## **7. Main Flow**

For each screen:
☐ Enter main flow (CTA)
☐ Create 1 item
☐ Edit
☐ Delete
☐ Flow doesn't freeze
☐ Layout doesn't break
☐ Navigation ok
☐ No ugly alerts

---

## **8. Spelling and Messages**

☐ Clear messages
☐ Not embarrassed to show to client
☐ Minimally professional titles and descriptions

---

## **9. Colors and Branding**

☐ No colors outside standard
☐ No raw Vuetify
☐ No bad contrast

---

## **10. Evidence**

☐ 1 screenshot per screen
☐ 1 short video of main flow
☐ Final test:

> "Would I show this to the client without fear?"
> ☐ If not → fix / report

---

## **11. Scope**

☐ What was fixed is **within** scope
☐ Everything **outside** scope was listed as
**"Out-of-scope items identified"**
☐ Nothing critical left without warning

---

## **12. Recipes (if applicable)**

☐ Checked if useful recipe exists in repo / permitted locations
☐ If I don't have access → followed manual
☐ If recipe exists → executed within scope

---

# **FINAL RESULT**

### Choose ONE:

### ✔ Output 1 — Documentation + Handoff

☐ Problems listed
☐ Evidence attached
☐ Task created in Jira
☐ Notice in Slack / Task
☐ Out-of-scope items listed

### ✔ Output 2 — Fix + Log

☐ Problems fixed
☐ Evidence attached
☐ Notice in Slack / Task
☐ Out-of-scope items listed
