---
id: extract-emails-from-remote-server-via-pop-imap-or-exchange-web-services-protocols
url: parser/java/extract-emails-from-remote-server-via-pop-imap-or-exchange-web-services-protocols
title: Extract emails from remote server via POP IMAP or Exchange Web Services protocols
weight: 6
description: ""
keywords: 
productName: GroupDocs.Parser for Java
hideChildren: False
---
GroupDocs.Parser provides the functionality to extract emails from remote servers. The following email protocols are supported:

*   Post Office Protocol (POP)
*   Internet Message Access Protocol (IMAP)
*   Exchange Web Services (EWS)

To create an instance of `[Parser](https://apireference.groupdocs.com/java/parser/com.groupdocs.parser/Parser)` class to extract emails from a remote server the following constructor is used:

```java
Parser(String filePath, LoadOptions loadOptions);

```

Here are the steps to extract emails from the remote server:

*   Prepare connection string (see table below);
*   Instantiate `[Parser](https://apireference.groupdocs.com/java/parser/com.groupdocs.parser/Parser)` object with connection string;
*   Call `**[isContainer](https://apireference.groupdocs.com/java/parser/com.groupdocs.parser.options/Features#isContainer())**()`  property to check if container extraction is supported;
*   Call `**[getContainer](https://apireference.groupdocs.com/java/parser/com.groupdocs.parser/Parser#getContainer())**()` method and obtain collection of `[ContainerItem](https://apireference.groupdocs.com/java/parser/com.groupdocs.parser.data/ContainerItem "class in com.groupdocs.parser.data")` objects;
*   Iterate through the collection and get `[Parser](https://apireference.groupdocs.com/java/parser/com.groupdocs.parser/Parser)` object for each item.

The following example shows how to extract emails from Exchange Server:

```java
StringBuilder sb = new StringBuilder();
sb.append("mode = exchange");
sb.append('\n');
sb.append("MailboxUri = https://outlook.office365.com/ews/exchange.asmx");
sb.append('\n');
sb.append("Username = email@server");
sb.append('\n');
sb.append("Password = password");
// Create an instance of Parser class to extract emails from the remote server
// As filePath connection parameters are passed; LoadOptions is set to Email file format
try (Parser parser = new Parser(sb.toString(), new LoadOptions(FileFormat.Email))) {
    // Check if container extraction is supported
    if (!parser.getFeatures().isContainer()) {
        System.out.println("Container extraction isn't supported.");
        return;
    }
    // Extract email messages from the server
    Iterable<ContainerItem> emails = parser.getContainer();
    // Iterate over attachments
    for (ContainerItem item : emails) {
        // Create an instance of Parser class for email message
        try (Parser emailParser = item.openParser()) {
            // Extract the email text
            try (TextReader reader = emailParser.getText()) {
                // Print the email text
                System.out.println(reader == null ? "Text extraction isn't supported." : reader.readToEnd());
            }
        }
    }
} 
```

The following connection parameters are used:

| Protocol | Parameters |
| --- | --- |
| POP | mode = pop  
Host = <url>  
Port = <port>  
Username = <user-name>  
Password = <password>  
  
 |
| IMAP | mode = imap  
Host = <url>  
Port = <port>  
Username = <user-name>  
Password = <password>  
  
 |
| EWS | mode = exchange  
MailboxUri = <url>  
Username = <user-name>  
Password = <password>
 |

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Parser for .NET examples](https://github.com/groupdocs-parser/GroupDocs.Parser-for-.NET)
    
*   [GroupDocs.Parser for Java examples](https://github.com/groupdocs-parser/GroupDocs.Parser-for-Java)
    

### Free online document parser App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to parse documents and extract data from PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Parser App](https://products.groupdocs.app/parser).