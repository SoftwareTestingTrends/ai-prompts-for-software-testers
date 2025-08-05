## **Form-Level Accessibility Audit Prompt**

**Task:**
1. **Perform an Accessibility Audit**
   Visit the following webpage:
   `<WEB_FORM_URL>` and audit the form for accessibility issues based on the checklist provided later in this document.
2. **Highlight Problem Areas Visually**
   For every accessibility issue detected, apply a visible CSS outline to the corresponding form element to help identify it directly on the page.
3. **Generate a Markdown Report**
   Summarize your findings in a well-structured Markdown file and save it using the following naming format:
   `YYYY-MM-DD_form-accessibility-report.md`

### **Form Accessibility Checklist**

#### 1. **Label Association**

* Ensure every form input (e.g., text fields, checkboxes, radios, selects) has an associated `<label>`.
* Verify labels are explicitly associated using `for` and `id` attributes or are correctly nested.
* Avoid using only placeholder text as a substitute for labels.

#### 2. **Field Instructions and Hints**

* Check that help text (e.g., input format instructions or guidance) is programmatically associated using `aria-describedby`.
* Confirm that required fields are clearly indicated with visible text and/or `aria-required="true"`.

#### 3. **Error Messages**

* Trigger validation errors (e.g., by submitting incomplete forms) and confirm that:

  * Errors are **visibly presented** next to the relevant field.
  * Errors are **announced by screen readers** (e.g., via `aria-live`, `aria-describedby`, or inline text).
  * Fields in error are marked with `aria-invalid="true"` and referenced with `aria-describedby`.

#### 4. **Keyboard Navigation**

* Ensure all fields, labels, and error messages are navigable and operable using a keyboard (Tab, Shift+Tab, Enter, Space).
* Verify that keyboard focus follows a logical order.

#### 5. **Focus Management**

* When a validation error occurs:

  * Focus should move to the first invalid field.
  * Upon successful submission, focus should move to a confirmation or success message.

#### 6. **Autocomplete & Input Types**

* Use appropriate HTML5 input types (`type="email"`, `type="tel"`, etc.) to enable better mobile and assistive tech support.
* Provide meaningful `autocomplete` attributes where relevant.

#### 7. **Accessible Grouping**

* Use `<fieldset>` and `<legend>` to group related fields (e.g., radio buttons, checkboxes).

#### 8. **Color & Visual Indicators**

* Avoid using color alone to indicate errors or required fields—ensure a secondary textual or symbolic cue (e.g., asterisk or icon with text).

---

### **Expected Output Format**

```markdown
## Form Accessibility Issues

### Missing Labels
- Input with `id="email"` is missing an associated `<label>`

### Error Handling Issues
- Required "Name" field produces a visible error but it is not announced to screen readers
- Error message lacks `aria-describedby` association

### Keyboard Navigation
- Tab order skips the "Phone Number" input

### Focus Management
- After form error, focus remains on submit button instead of moving to first invalid field

### Other
- No `autocomplete` on address fields
- Related radio buttons are not grouped using `<fieldset>`
```

### Output Report:
Save the output as a markdown report file `YYYY-MM-DD_form-accessibility-report.md`
