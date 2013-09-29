Usage
=====

There's already a perfect article on [how to use pdf2htmlEX in command line](https://github.com/coolwanglu/pdf2htmlEX/wiki/QuickStart).

Usage of the webapp testing suite is very much simple:

1. [Install](install.md) the application.
2. Open the application with your web browser.
3. If you wish to upload large PDF files, don't forget to increase the size limit in PHP options.
4. Choose a file in file selection widget.
5. Hit the green "Submit" button.
6. pdf2htmlEX will be launched and your file will be converted.

You'll see a table with a list of uploaded files. Each file has a status:

* `processing` if pdf2htmlEX is currently working on your file. Reload the page until the status changes. Do NOT resubmit the file on reload, it's already there;
* `converted` if pdf2htmlEX has successfully converted your file. In this case, you'll see a link to HTML version next to a link to PDF version;
* `broken` if pdf2htmlEX was unable to convert the file or if converted version was removed from server.

In case of any problem, the system will show somehow verbose error message. However, this should not happen if you've installed the application correctly and are uploading a valid PDF file.