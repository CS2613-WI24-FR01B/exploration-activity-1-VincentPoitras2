# Overview
With this package, a few answers had to be answered to futhur understand this package  

## What purpose does it serve?
The purpose for this package is to change, add, transform, basically anything to do with a pdf file. So many things can be done with this program, here are a few examples:  
1.  Can provide a pdf's metadata (author, creator, producer, subject, title).
```
from pypdf import PdfReader

reader = PdfReader("example.pdf")

meta = reader.metadata

print(len(reader.pages))

# All of the following could be None!
print(meta.author)
print(meta.creator)
print(meta.producer)
print(meta.subject)
print(meta.title)
```
 It can also write these detail into a pdf file.
 ```
 from datetime import datetime
from pypdf import PdfReader, PdfWriter

reader = PdfReader("example.pdf")
writer = PdfWriter()

# Add all pages to the writer
for page in reader.pages:
    writer.add_page(page)

# If you want to add the old metadata, include this line
metadata = reader.metadata
writer.add_metadata(metadata)

# Format the current date and time for the metadata
utc_time = "-05'00'"  # UTC time optional
time = datetime.now().strftime(f"D\072%Y%m%d%H%M%S{utc_time}")

# Add the new metadata
writer.add_metadata(
    {
        "/Author": "Martin",
        "/Producer": "Libre Writer",
        "/Title": "Title",
        "/Subject": "Subject",
        "/Keywords": "Keywords",
        "/CreationDate": time,
        "/ModDate": time,
        "/Creator": "Creator",
        "/CustomField": "CustomField",
    }
)

# Save the new PDF to a file
with open("meta-pdf.pdf", "wb") as f:
    writer.write(f)
```
2.  Text extraction 
3.  
 ADD EXAMPLES OF OUTPUT  

## Addional Comments
As a student, almost every submission file for homework involves pdf's. Manipulating these files can be hard so the manipulation of pdfs can be very useful. This is one of the main reasons why I decided to chose this package that was created July 7th, 2015. Also, my summer job requires automation of invoices that are sent by email in pdf forms. I have been using excel- (VBA) for this process and it is very cool to see that this process can be done in python with a much wider variety of operations.  
This package has further influenced my learning for this language since it can be used much more than a computational programming language. In first year, I have used python in a class which was purely computational and file I/O purposes. I can now say that Python can be also used as a object oriented programming language.  
My overall experience with this package was succesful and fun. I had no clue that so many things could be done to a pdf file in order to change its sturcture. I would recommend this package to anyone who uses pdfs files in some sort of automation process. I will definitely use this package later on for my summer job since a huge role in the company is to automate the process of ordering and creating invoices. This package will be very useful to manipulate these pdf files since it has more room for manipulating the files to my liking.