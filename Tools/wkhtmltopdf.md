`brew install wkhtmltopdf` this won't work 

use this:
```bash
curl -L https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-2/wkhtmltox-0.12.6-2.macos-cocoa.pkg -O

installer -pkg wkhtmltox-0.12.6-2.macos-cocoa.pkg -target ~
```