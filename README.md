Spreadsheets.Bills
==================

![Overview](https://raw.githubusercontent.com/ernesthwang/Spreadsheets.Bills/master/doc/images/Screenshot01.png "Overview")

This is an Excel spreadsheet that can be used to keep track of your recurring expenditures, including weekly, monthly, quarterly and annual expenditures (there's really no limit to the recurring nature of your bills).  The primary purpose of this spreadsheet is to give you visual indicators on upcoming and late bills.

Other features include:
* Sum of total expenditures per vendor
* Displays how many days since last payment

## How to use this spreadsheet

### Set the initial dates
Pick a date approximately 30 days from the day you start tracking.  This way, you don't start with a blank spreadsheet.  I figure a month is pretty easy to fill out, because you most likely need to look at one bank statement to back-fill the data in the spreadsheet.

### Set your column values
Figure out what your recurring bills are and enter the following:
* Name (Row 8)
* Payment Threshold in Days (Row 4)
* Due Date/Day/Month (Row 6)

There is more information about what these values mean in the Table Data section below.

When overwriting columns, start on the left and add new vendors to the right.  Don't delete the first column of a section, because it also contains the Cycle name (e.g. "Monthly").  Don't delete the spacer column that separates two sections (e.g. Column E), because you're going to want to copy that column when you add new vendors.

### Delete unused sample vendors
So you've entered all your bill recipients and you have a few columns left over?  Delete them.  But make sure you leave a space between sections.  If you're not using a section (e.g. You don't have any bills that are due weekly), then go ahead and delete that section along with the spacer column.

### Start entering data!
This is where the fun begins!  Check your last bank statement.  Log into your bank's web site.  Log into mint.com.  Check your Quicken Home & Business reports (Do people still use Quicken?).  Find the data you need and enter it in the appropriate cells.  Just enter the amount in the cell that corresponds to the vendor and date.  In the screenshot above, the cell G167 corresponds to a $120 cable bill payment made on 6 Feb 2014.


## Table Data

### Rows
#### Row 1: Cycle Name
Just a label indicating the type of bill you are tracking.  This currently includes:
* Weekly
* Monthly
* Quarterly
* Semi-Annually
* Annually

These are just labels.  The actual cycles of the bills are set by the values in Row 4: Threshold

#### Row 2: Days Tracked
This is primarily a blank row.  I may remove it in the interest of preserving space.  This row *does* contain the total numbers of days tracked, though.

The formula for cell C2 is

`=SUM(C9:C1048576)`

#### Row 3: Warning Indicator
If a bill's due date is fast approaching, the cell in this row will have a pink background with a single "!" character in it.

![!](https://raw.githubusercontent.com/ernesthwang/Spreadsheets.Bills/master/doc/images/Screenshot02.png "!")

If the bill's due date is past, then this cell will have a red background and a bold "!!" value.

![!!](https://raw.githubusercontent.com/ernesthwang/Spreadsheets.Bills/master/doc/images/Screenshot03.png "!!")

#### Row 4: Threshold
Input the number that corresponds to how often the bill should be paid.  Suggestions are as follows:
* Weekly: 7
* Monthly: 30 (don't worry, this doesn't have to be exact)
* Quarterly: 75-80
* Annually: 350

You don't have to put the exact value here.  I prefer to shave a few days off depending on the cycle of the bill.  It's usually a lot more important to pay an annual bill on time as opposed to paying some weekly or monthly bill on time.

#### Row 5: Days Since
This row displays the number of days that have passed since the last payment.

The formula for cell C5 is

`=ROW(INDEX(C:C,MATCH(9.99999999999999E+307,C:C)))`

The formula for cell D5 is

`=$C5 - ROW(INDEX(D:D,MATCH(9.99999999999999E+307,D:D)))`


#### Row 6: Due Label
There is no formula attached to this row.  You can just type whatever value you want to help you rememeber on what day the bill is due.  In the Monthly section, you'd probably put the day of the month.  In the Annual section, you'd probably put the month.

#### Row 7: Lifetime Expenditure
This is the total that you have paid to the vendor in question since tracking.

The formula for cell D7 is

`=SUM(D9:D1048576)`

#### Row 8: Vendor Name
Enter the name of the vendor or just a keyword (e.g. "Electricity" instead of "Southern California Edison").  The more concise you can be the better, because this row is rotated 90 degrees to keep the columns spaced equally.  A long name can greatly reduce how much you can see on the screen.

#### Rows 9+: Data
Here's where you enter your data.

### Columns

#### Column A: Day of Week
This is a duplicate of column B, just formatted differently.

The formula for cell A9 is
`=B9`

#### Column B: Date
You need to seed this column with values that reflect your start date.  Cell B9 should be approximately one month before your start date.  Then you would need to back-fill the data in the first 30 data rows.

You should only need to set the value of cell B9.  There are formulas in cells B10 and higher that just add one day to the column above it.  The formula for cell B10.

`=B9 + 1`

NOTE: I am currently trying to figure out a way to have the values turn blue for Saturday and Sunday using conditional formatting.  If your start date isn't a Monday, your dates will look goofy.


#### Column C: "Day Has Occurred" Flag
This is a calculated field that has a green background and displays the value "1" once the day has come.  Even though this column may look empty, there should be values for every day.  The formula for the cell in this column should be

`=IF(B9 <= NOW(), 1, "")`

Where B9 corresponds to the date cell in Row 9.

#### Columns D+: Data
Here's where you enter your data.


## Notes

### Be careful when copying/pasting
What looks like a blank cell might actually contain data.  Also, some of the blank cells may have some formatting in it that needs to be copied.  If you want to add new columns, your best bet is to copy the blank column for that section and perform an Insert Paste to preserve formatting.


### Make sure new dates contain expected formulae
If you run out of dates, you can add more, but make sure you copy the formulas in columns A and C.


### Why isn't this spreadsheet in Google Docs?
I've tried to convert this document for use in Google Docs, but I ran into two main issues.

Google Spreadsheets doesn't support some of the formulae used here, such as MATCH and ROW (not 100% sure about ROW, though).

Google Spreadsheets don't like large files.  My current spreadsheet has 1800 rows in it and I've found Google Spreadsheets to be very slow when navigating large documents.

It's been a while since I've tried converting this, so some of these issues may have been resolved, but migrating this would be a project that I tackle in the future.  Besides, I love Excel.
