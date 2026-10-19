# Task 3 — problems in the café form

| # | Line of code | Why it is a problem for the user | How I fixed it |
|---|---|---|---|
| 1 | `<input type="text" placeholder="Your name">` | Only a placeholder: it disappears when typing, screen readers may not announce it, low contrast. No `name`, so the value is never sent. | Added `<label for="name">`, `id="name"`, `name="name"`, `autocomplete="name"`, `required`. |
| 2 | `<input type="text" placeholder="Email">` | Same problems; type `text` gives no email keyboard on a phone and no format check. | `type="email"` + label + `name` + `required`. |
| 3 | `<label>Phone</label>` | Label has no `for`: a click on it does not focus the field, a screen reader does not link them. | `<label for="phone">` matching `id="phone"`. |
| 4 | `<input type="text" id="phone">` | No `name` (data not sent); `text` shows a full keyboard on a phone. | `type="tel"`, `name="phone"`, `autocomplete="tel"`. |
| 5 | `<label for="guests">` + `<input id="people">` | `for` and `id` do not match: the label is connected to nothing. Also no `name`. | Same id in both: `id="guests"`, `name="guests"`. |
| 6 | `<input type="text" id="people">` | Guests is a number, but any text can be typed, and no numeric keyboard. | `type="number" min="1" max="20" required`. |
| 7 | `<input type="text" id="date" placeholder="dd/mm/yyyy">` | User must guess the format; wrong dates are accepted; no `name`. | `type="date"` (native picker, format check), `name="date"`, `required`. |
| 8 | `id="date"` on the "Inside" radio | Duplicate id: invalid HTML, and `label for="date"` becomes ambiguous (can focus the wrong control). | Unique ids: `inside`, `terrace`. |
| 9 | `name="inside"` / `name="terrace"` | Different names, so they are not one group: both can be chosen, arrow keys do not move between them. No `value`, so nothing useful is sent. | One name `seating`, values `inside` / `terrace`. |
| 10 | `<p>Seating:</p>` | A screen reader does not know the radios belong to this question. | `<fieldset>` + `<legend>Seating</legend>`. |
| 11 | `<input type="radio"> Inside` | Text is not inside a label: tiny click target, not announced. | `<label class="form-check-label" for="inside">`. |
| 12 | `<select><option>Lunch…` | No label, no `name` (choice not sent), options without `value`. | `<label for="meal">`, `name="meal"`, `value` on every option. |
| 13 | `<textarea placeholder="Comments">` | Placeholder only, no `name`: comments are lost. | Label + `id="comments"` + `name="comments"`. |
| 14 | `<input type="checkbox"> I agree…` | No label (hard to tap), no `name`, not required: the user can send without agreeing. | `<label for="terms">`, `name="terms"`, `required`. |
| 15 | `<div class="btn btn-primary">Reserve</div>` | A `div` cannot get focus with Tab and Enter does nothing; it does not submit the form. Keyboard and screen-reader users cannot reserve. | `<button type="submit" class="btn btn-primary">`. |
| 16 | whole `<form>` | No Bootstrap form classes: fields are not full width, cramped on a phone. No required fields. | Bootstrap grid, `form-control`, `form-select`, `form-check`, `mb-3`; `required` on the important fields. |

## Two problems with another possible fix

**Problem 15 (the "Reserve" div).**
Other fix: keep the `div` and add `role="button" tabindex="0"` plus JavaScript for Enter/Space to submit.
Why mine is better: `<button type="submit">` already gives focus, Enter/Space, submit and screen-reader role with no extra code. The `div` version needs JavaScript, which is easy to break (and not allowed in this assignment).

**Problem 9 (two radio groups).**
Other fix: replace the radios with `<select name="seating">` (Inside / Terrace).
Why mine is better: only two choices, so radios show both options at once and need one click instead of two. The select is a good choice only if there were many places.
