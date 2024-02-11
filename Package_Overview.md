# Overview
With this package, a few answers had to be answered to futhur understand this package  

## What purpose does it serve?
The purpose for this package is to change, add, transform, basically anything to do with a pdf file. So many things can be done with this program, here are a few examples using the first page of the course syllabus of CS2613:  
1.  Can provide a pdf's metadata (author, creator, producer, subject, title).  
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
        "/Author": "Vincent Poitras",
        "/Producer": "UNB",
        "/Title": "Meta Data Example",
        "/Subject": "CS2613",
        "/Keywords": "Example",
        "/CreationDate": time,
        "/ModDate": time,
        "/Creator": "Vincent Poitras",
        "/CustomField": "Example",
    }
)

# Save the new PDF to a file
with open("meta-pdf.pdf", "wb") as f:
    writer.write(f)
```  
To get the information, use the following code
```
from pypdf import PdfReader

reader = PdfReader("example.pdf")

meta = reader.metadata

# All of the following could be None!
print(meta.author)
print(meta.creator)
print(meta.producer)
print(meta.subject)
print(meta.title)
```
![alt text](example1.png)

2.  Text extraction 
```
from pypdf import PdfReader

reader = PdfReader("example.pdf")
page = reader.pages[0]
print(page.extract_text())
```
![alt text](example2.png)  
3.  Transforming several pages  
```
from pypdf import PdfReader, PdfWriter, Transformation, PaperSize

# Read source file
reader = PdfReader("nup-source.pdf")
sourcepage = reader.pages[0]

# Create a destination file, and add a blank page to it
writer = PdfWriter()
destpage = writer.add_blank_page(width=PaperSize.A4.height, height=PaperSize.A4.width)

# Copy source page to destination page, several times
for x in range(4):
    for y in range(4):
        destpage.merge_transformed_page(
            sourcepage,
            Transformation().translate(
                x * sourcepage.mediabox.width,
                y * sourcepage.mediabox.height,
            ),
        )

# Write file
with open("nup-dest2.pdf", "wb") as fp:
    writer.write(fp)
```
![alt text](example3.png)  
This page is not a great example for this application, but it shows how this can be used  
4.  Removing Images
```
from pypdf import PdfReader, PdfWriter

reader = PdfReader("example.pdf")
writer = PdfWriter()

for page in reader.pages:
    writer.add_page(page)

writer.remove_images()

with open("out.pdf", "wb") as f:
    writer.write(f)
```
![alt text](example4.png)

## Addional Comments
As a student, almost every submission file for homework involves pdfs. Manipulating these files can be hard so a process to manipulate these pdfs can be very useful. This is one of the main reasons why I decided to chose this package that was created July 7th, 2015. Also, my summer job requires automation of invoices that are sent by email in pdf forms. I have been using excel (VBA) for this process and it is very cool to see that this process can be done in python with a wider variety of operations.  
This package has further influenced my learning for this language since Python can be used much more than a computational programming language. In first year, I have used python in a class which was purely computational and file I/O purposes. I can now say that Python can be also used as a object oriented programming language.  
My overall experience with this package was succesful and fun. I had no clue that so many things could be done to a pdf file in order to change its sturcture. I would recommend this package to anyone who uses pdfs files in some sort of automation process. I will definitely use this package later on for my summer job since a huge role in the company is to automate the process of ordering and creating invoices. This package will be very useful to manipulate these pdf files since it has more room for manipulating the files to my liking.