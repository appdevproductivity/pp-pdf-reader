<section class="pp-page-header">
  <img src="../app-icon/Icon-120.png" alt="Paper & Pencil PDF Reader app icon">
  <div>
    <p class="pp-kicker">Contact Us</p>
    <h1>Send feedback, report a bug, or suggest a feature.</h1>
  </div>
</section>

<section class="pp-contact-layout">

  <form class="pp-contact-form" id="pp-contact-form">

    <label for="contact-email">Your email</label>
    <input id="contact-email" name="email" type="email" autocomplete="email" required placeholder="you@example.com">

    <label for="contact-topic">Topic</label>
    <select id="contact-topic" name="topic" required>
      <option value="Bug report">Bug report</option>
      <option value="Feature suggestion">Feature suggestion</option>
      <option value="Other topic">Other topic</option>
    </select>


    <label for="contact-subjectdetail">Subject:</label>
    <input id="contact-subjectdetail" name="subjectdetail" required>

    <label for="contact-message">Message</label>
    <p class="pp-contact-help" id="bug-report-help">For bug report, indicate in detail the steps to replicate the bug.</p>
    <textarea id="contact-message" name="message" rows="8" required placeholder="Tell us what happened, what you expected, or what you would like to see."></textarea>

    <button class="md-button md-button--primary" type="submit">Compose Email</button>
  </form>

  <aside class="pp-contact-note">
    <h2>What happens next?</h2>
    <p>
      The form opens your email app with the message.
      Review the email and send it from your own mail account.
    </p>
  </aside>
</section>

<script>
  (function () {
    var form = document.getElementById("pp-contact-form");
    var topicField = document.getElementById("contact-topic");
    var subjectDetailField = document.getElementById("contact-subjectdetail");
    var messageField = document.getElementById("contact-message");
    var bugReportHelp = document.getElementById("bug-report-help");
    var defaultMessagePlaceholder = "Tell us what happened, what you expected, or what you would like to see.";
    var bugReportMessagePlaceholder = "Report the steps to replicate the bug in detail.";

    if (!form || !topicField || !subjectDetailField || !messageField || !bugReportHelp) {
      return;
    }

    function updateMessagePlaceholder() {
      var isBugReport = topicField.value === "Bug report";

      messageField.placeholder = isBugReport ?
        bugReportMessagePlaceholder :
        defaultMessagePlaceholder;
      bugReportHelp.hidden = !isBugReport;
    }

    topicField.addEventListener("change", updateMessagePlaceholder);
    updateMessagePlaceholder();

    form.addEventListener("submit", function (event) {
      event.preventDefault();

      if (!form.reportValidity()) {
        return;
      }

      var topic = topicField.value;
      var subjectdetail = subjectDetailField.value.trim();
      var email = document.getElementById("contact-email").value.trim();
      var message = messageField.value.trim();
      var subject = "[" + topic + "] " + subjectdetail;
      var body = [
        message
      ].join("\n");

      window.location.href = "mailto:contact@pp-pdf-reader.com?subject=" +
        encodeURIComponent(subject) + "&body=" + encodeURIComponent(body);
    });
  }());
</script>
