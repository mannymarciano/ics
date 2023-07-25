Here is the README documentation formatted as a Markdown (.md) file:

# Calendar ICS File Generator

This is a simple script to generate and download a .ics calendar file using HTML and JavaScript.

## Usage

The script contains a sample event that can be customized. To trigger the download, click the "Download ICS" button. 

This will generate the .ics file data, create a blob URL for it, generate a temporary link element to trigger the download, and clean up afterwards.

The user will be prompted to download the `event.ics` file or open it in their calendar app.

## Code Overview

### HTML

The HTML contains a button to trigger the download and an empty script tag for the JavaScript code.

```html
<button id="download">Download ICS</button>

<script></script>
```

### JavaScript

The JavaScript handles generating the .ics file data, downloading it, and cleaning up.

**Generate .ics data**

This uses the .ics file format specification to create the event data:

```js
const icsData = `BEGIN:VCALENDAR 
// Rest of event data
END:VCALENDAR`
```

**Download handler**

This is triggered on click of the download button:

```js
downloadButton.addEventListener('click', () => {

  // 1. Generate blob URL from ics data
  const blob = new Blob([icsData], {type: 'text/calendar;charset=utf-8'})
  const url = URL.createObjectURL(blob);

  // 2. Create and click temporary link to download
  const a = document.createElement('a');
  a.setAttribute('download', 'event.ics');
  a.setAttribute('href', url);
  document.body.appendChild(a);
  a.click();

  // 3. Cleanup
  document.body.removeChild(a);
  URL.revokeObjectURL(url);

})
```

This uses the Blob API and URL.createObjectURL to generate a downloadable link for the .ics data generated.

### Customizing

To customize the generated event, modify the icsData variable with different event details. Refer to the .ics format specification for supported fields.

## References

- [.ics format specification](https://icalendar.org/iCalendar-RFC-5545/3-4-definition-of-icalendar-object.html)
- [MDN Web Docs - Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob) 
- [MDN Web Docs - URL.createObjectURL()](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL)

Let me know if you have any other questions!
