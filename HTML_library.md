# [W3 HTML Manual](https://www.w3schools.com/html/)

## HTML Quiz
### First Quiz Set

#### Question 1: Default TCP/IP Port
**Q: When a browser connects to a web server to retrieve a document, what is the default TCP/IP port that is used?**

**A: 80**

**Explanation:** The default port for HTTP (HyperText Transfer Protocol) is port 80. When a browser requests a document over HTTP, it connects to this port unless a different port is specified in the URL.

#### Question 2: Browser Request Command
**Q: When a browser connects to a web server to retrieve a document, what command is sent to the server?**

**A: GET**

**Explanation:** The GET request is the HTTP method used by browsers to retrieve documents or data from a web server.

#### Question 3: Browser Display Header
**Q: Which of the HTTP headers does the browser look at to decide how to display the retrieved document?**

**A: Content-type**

**Explanation:** The Content-type header tells the browser the type of content being returned, like HTML, JSON, or images, so it knows how to render or handle the document.

#### Question 4: HTTP "T" Meaning
**Q: What does the second "T" of HTTP stand for?**

**A: Transfer**

**Explanation:** The second "T" in HTTP stands for Transfer, as in HyperText Transfer Protocol. It refers to the transfer of data over the internet, specifically HTML documents.

#### Question 5: URL Components
**Q: Which of the following is NOT part of a Uniform Resource Locator?**

**A: Operating system**

**Explanation:** A Uniform Resource Locator (URL) contains parts like the protocol, domain, and path, but it does not include the operating system of the server.

#### Question 6: HTML Tags Generating Requests
**Q: Which HTML tags typically generate a request to retrieve a document?**

**A: `<a>` and `<img>`**

**Explanation:** The `<a>` (anchor) tag generates a request when linking to another page, and the `<img>` tag generates a request to load an image from a server.

#### Question 7: Internet Protocol Standards
**Q: What standards organization publishes many of the documents that describe the protocols we use on the Internet?**

**A: IETF**

**Explanation:** The Internet Engineering Task Force (IETF) is responsible for publishing the specifications and protocols used to ensure the functionality of the internet.

### Second Quiz Set

#### Question 1: Absolute Reference
**Q: What is true about the following HTML?**
```html
<a href="http://www.dr-chuck.com/page2.htm">Second Page</a>
```

**A: The reference is an absolute reference**

**Explanation:** An absolute reference includes the full URL (starting with http:// or https://) to a webpage or resource. In this example, the href attribute points to a specific address, making it an absolute URL.

#### Question 2: DOCTYPE Declaration
**Q: What do you put at the beginning of an HTML file to inform the browser which variant of HTML you will be using in this document?**

**A: DOCTYPE**

**Explanation:** The DOCTYPE declaration at the start of an HTML document tells the browser what version of HTML to expect, ensuring correct rendering. For example, `<!DOCTYPE html>` specifies HTML5.

#### Question 3: Page Title Tag
**Q: What is the name of the tag that is used in a document's `<head>` area to set the text shown in the tab of the browser or title bar?**

**A: `<title>`**

**Explanation:** The `<title>` tag, located within the `<head>` section, defines the title of the webpage that appears in the browser's tab or title bar.

#### Question 4: Image Alt Text
**Q: In HTML, what attribute is used to indicate text that will be shown if an image is not loaded or read to a user that is using a screen reader?**

**A: alt**

**Explanation:** The alt attribute provides alternative text for images, which is displayed if the image fails to load and read by screen readers for accessibility.

#### Question 5: HTML Attributes
**Q: For the following HTML:**
```html
<img src="csev_ian_dolphin_small.jpg" alt="Photo Credit: Ian Dolphin" width="160" align="middle">
```
**What is an example of an "attribute"?**

**A: src**

**Explanation:** In HTML, an attribute is a property added to a tag to provide additional information. In this example, src specifies the source of the image file.

#### Question 6: Less-Than Symbol
**Q: How do you show a less-than (`<`) in an HTML page?**

**A: `&lt;`**

**Explanation:** In HTML, special characters like `<` need to be escaped using entities. `&lt;` is the entity code for the less-than symbol to ensure it displays correctly.

#### Question 7: Unordered List Tag
**Q: What does the `<ul>` tag accomplish?**

**A: Begins an unordered list**

**Explanation:** The `<ul>` tag creates an unordered list in HTML. Items within the list are typically marked with bullets and are represented by `<li>` tags.

#### Question 8: Table Tag Order
**Q: In a table, what is the general order of tags from outer to inner when constructing a table?**

**A: `<table>`, `<tr>`, `<td>`**

**Explanation:** When constructing a table in HTML, the order is as follows:
- `<table>`: This is the outermost tag that defines the entire table.
- `<tr>`: This tag defines a row within the table.
- `<td>`: This tag defines a cell within a row.
So, the hierarchy goes from `<table>` (container for the whole table) to `<tr>` (table rows) and then to `<td>` (individual cells in the row).
