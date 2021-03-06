Note: As of v0.10.0, SPUtility.js supports both the 12 hour format (3/14/2014 1:00 AM) and the 24 hour format (14/03/2014 01:00).

**Note for those using a 24 hour date format:** By default, SPUtility.js uses the 12 hour date format. You will need to call SetTimeFormat before the rest of your code to use the 24 hour date format:

SPUtility.SetTimeFormat('24HR');

If you use a separator other than a "/" for your dates, for example 10.03.2015, then call SetDateSeparator:

SPUtility.SetDateSeparator('.');

### Date
{{
// Date fields (no time value)
var myDateField = SPUtility.GetSPField('Date Field');

// Set the year (2010), month (august), day (13)
myDateField.SetValue(2010, 8, 13);

// GetValue returns a SPDateTimeFieldValue object
// Note: As of 0.9.1, the properties will always be numbers (not strings)
var value = myDateField.GetValue();
// value.Year = 2014
// value.Month = 3
// value.Day = 14
// value.IsTimeIncluded = false
// Note: As of 0.10.0, there is a new TimeFormat property for 12HR or 24HR formats
// value.TimeFormat = '12HR'
// value.toString() => '3/14/2014'
// ----- or ----
// value.TimeFormat = '24HR'
// value.toString() => '14/03/2014'


// Make the field read only
myDateField.MakeReadOnly();

// Hide the field
myDateField.Hide();
}}
### Date and Time
{{
// Date & Time field
var myDateTimeField = SPUtility.GetSPField('Date Time Field');

// Sets the value to 8/13/2010 1:30PM
// Should match the values in the time dropdowns
//  Hour Ex: 12 PM or 3 AM
//  Time Ex: 00, 25, 35 (increments of 5 from 00 to 55)
// Last two parameters should be strings
myDateTimeField.SetValue(2010, 8, 12, '3 PM', '55');

// Gets a SPDateTimeFieldValue object
// Note: As of 0.9.1, the properties will always be numbers (not strings)
var value = myDateTimeField.GetValue();
// value.Year = 2010
// value.Month = 8
// value.Day = 12
// value.Hour = 15
// value.Minute = 55
// value.IsTimeIncluded = true
// value.toString() => 8/12/2010 3:55PM

// Set only the date portion (as of 0.9.1)
myDateTimeField.SetDate(2010, 8, 12);

// Set only the time portion using numbers or strings! (as of 0.9.1)
myDateTimeField.SetTime(8, 30); // 8:30 AM
myDateTimeField.SetTime(15, 0); // 3:00 PM
myDateTimeField.SetTime('5 PM', '55'); // 5:55 PM

// Make the field read only
myDateTimeField.MakeReadOnly();

// Hide the field
myDateTimeField.Hide();
}}
Set a DateTime field to "now":
{{
// default contact date to "today"
var today = new Date();
var hour = today.getHours();
if (hour > 12) {
	hour = (hour - 12) + " PM";
} else {
	hour += " AM";
}
// round the current minute down to the nearest 5 minutes
var minute = today.getMinutes();
minute = minute - (minute % 5);
SPUtility.GetSPField('Contact Date').SetValue(today.getFullYear(), today.getMonth()+1, today.getDate(), hour, minute);
}}