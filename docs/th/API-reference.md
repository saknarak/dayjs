# API Reference

Day.js เป็น library ที่สร้างครอบ `Date` อ็อบเจกต์ เรียกว่า `Dayjs` อ็อบเจกต์ แทนที่จะเป็นการแก้ไข `Date.prototype` โดยตรง

`Dayjs` เป็นอ็อบเจกต์แบบ immutable นั่นคือ เมื่อมีการเปลี่ยนแปลงค่าภายในอ็อบเจกต์ จะคืนค่าเป็นอ็อบเจกต์ใหม่เสมอ โดยไม่แก้ไขค่าในอ็อบเจกต์เดิม

- [API Reference](#api-reference)
  - [Parsing](#parsing)
    - [Constructor `dayjs(existing?: string | number | Date | Dayjs)`](#constructor-dayjsexisting-string--number--date--dayjs)
      - [ISO 8601 string](#iso-8601-string)
      - [Unix Timestamp (milliseconds since the Unix Epoch - Jan 1 1970, 12AM UTC)](#unix-timestamp-milliseconds-since-the-unix-epoch---jan-1-1970-12am-utc)
      - [Native Javascript Date object](#native-javascript-date-object)
    - [Clone `.clone() | dayjs(original: Dayjs)`](#clone-clone-dayjsoriginal-dayjs)
    - [Validation `.isValid()`](#validation-isvalid)
  - [Get and Set](#get-and-set)
    - [Year `.year()`](#year-year)
    - [Month `.month()`](#month-month)
    - [Day of the Month `.date()`](#day-of-the-month-date)
    - [Day of the Week `.day()`](#day-of-the-week-day)
    - [Hour `.hour()`](#hour-hour)
    - [Minute `.minute()`](#minute-minute)
    - [Second `.second()`](#second-second)
    - [Millisecond `.millisecond()`](#millisecond-millisecond)
    - [Set `.set(unit: string, value: number)`](#set-setunit-string-value-number)
  - [Manipulating](#manipulating)
    - [Add `.add(value: number, unit: string)`](#add-addvalue-number-unit-string)
    - [Subtract `.subtract(value: number, unit: string)`](#subtract-subtractvalue-number-unit-string)
    - [Start of Time `.startOf(unit: string)`](#start-of-time-startofunit-string)
    - [End of Time `.endOf(unit: string)`](#end-of-time-endofunit-string)
  - [Displaying](#displaying)
    - [Format `.format(stringWithTokens: string)`](#format-formatstringwithtokens-string)
      - [List of all available formats](#list-of-all-available-formats)
    - [Difference `.diff(compared: Dayjs, unit: string (default: 'milliseconds'), float?: boolean)`](#difference-diffcompared-dayjs-unit-string-default-milliseconds-float-boolean)
    - [Unix Timestamp (milliseconds) `.valueOf()`](#unix-timestamp-milliseconds-valueof)
    - [Unix Timestamp (seconds) `.unix()`](#unix-timestamp-seconds-unix)
    - [Days in the Month `.daysInMonth()`](#days-in-the-month-daysinmonth)
    - [As Javascript Date `.toDate()`](#as-javascript-date-todate)
    - [As Array `.toArray()`](#as-array-toarray)
    - [As JSON `.toJSON()`](#as-json-tojson)
    - [As ISO 8601 String `.toISOString()`](#as-iso-8601-string-toisostring)
    - [As Object `.toObject()`](#as-object-toobject)
    - [As String `.toString()`](#as-string-tostring)
  - [Query](#query)
    - [Is Before `.isBefore(compared: Dayjs)`](#is-before-isbeforecompared-dayjs)
    - [Is Same `.isSame(compared: Dayjs)`](#is-same-issamecompared-dayjs)
    - [Is After `.isAfter(compared: Dayjs)`](#is-after-isaftercompared-dayjs)
    - [Is Leap Year `.isLeapYear()`](#is-leap-year-isleapyear)
  - [Plugin APIs](#plugin-apis)
    - [RelativeTime](#relativetime)

## Parsing

### Constructor `dayjs(existing?: string | number | Date | Dayjs)`

เรียกใช้โดยไม่ระบุพารามิเตอร์ จะเป็นการสร้างอ็อบเจกต์ `Dayjs` ที่มีค่าเป็นวันเวลาปัจจุบัน

```js
dayjs();
```

Day.js ยังสามารถตีความรูปแบบวันที่ได้หลายรูปแบบ ตัวอย่างเช่น

#### [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string

```js
dayjs('2018-04-04T16:00:00.000Z');
```

#### Unix Timestamp (milliseconds since the Unix Epoch - Jan 1 1970, 12AM UTC)

```js
dayjs(1318781876406);
```

#### Native Javascript Date object

```js
dayjs(new Date(2018, 8, 18));
```

### Clone `.clone() | dayjs(original: Dayjs)`

คืนค่าอ็อบเจกต์โคลนของ `Dayjs`.

```js
dayjs().clone();
dayjs(dayjs('2019-01-25')); // passing a Dayjs object to a constructor will also clone it
```

### Validation `.isValid()`

คืนค่าชนิด `boolean` เพื่อแสดงว่าวันที่ของ `Dayjs` ถูกต้องหรือไม่.

```js
dayjs().isValid();
```

## การกำหนดค่าและการอ่านค่า

### ปี `.year()`

คืนค่าชนิด `number` เป็น ปี ค.ศ.

```js
dayjs().year();
```

### เดือน `.month()`

คืนค่าชนิด `number` เป็นเลขเดือน 0 คือ มกราคม.

```js
dayjs().month();
```

### วันที่ของเดือน `.date()`

คืนค่าชนิด `number` แสดงวันที่ของเดือน เช่น 1-31.

```js
dayjs().date();
```

### วันที่ของสัปดาห์ `.day()`

คืนค่าชนิด `number` เป็นค่าวันที่ของสัปดาห์ 0 คือวันอาทิตย์

```js
dayjs().day();
```

### ชั่วโมง `.hour()`

คืนค่าชนิด `number` เป็นค่าเวลาชั่วโมง 0-23

```js
dayjs().hour();
```

### นาที `.minute()`

คืนค่าชนิด `number` เป็นค่าเวลานาที 0-59

```js
dayjs().minute();
```

### วินาที `.second()`

คืนค่าชนิด `number` เป็นค่าเวลาวินาที 0-59

```js
dayjs().second();
```

### มิลลิวินาที `.millisecond()`

คืนค่าชนิด `number` เป็นค่าเวลามิลลิวินาทีวินาที 0-999

```js
dayjs().millisecond();
```

### ตั้งค่า `.set(unit: string, value: number)`

คืนค่าเป็น อ็อบเจกต์ของ `Dayjs` ที่มีต่าใหม่ตามที่กำนหด.

```js
dayjs('2000-10-25')
  .set('month', 3)
  .set('year', 2020).toString(); // Sat, 25 Mar 2020 00:00:00 GMT
```

## การแก้ไขค่า

อ็อบเจกต์ `Dayjs` สามารถถูกแก้ไขค่าได้หลายวิธี.

```js
dayjs('2019-01-25')
  .add(1, 'day')
  .subtract(1, 'year').toString(); // Fri, 26 Jan 2018 00:00:00 GMT
```

### เพิ่ม `.add(value: number, unit: string)`

คืนค่าเป็น อ็อบเจกต์โคลนของ `Dayjs` เป็นวันที่เวลา with a specified amount of time added.

```js
dayjs().add(7, 'day');
```

### Subtract `.subtract(value: number, unit: string)`

Returns a cloned `Dayjs` with a specified amount of time subtracted.

```js
dayjs().subtract(7, 'year');
```

### Start of Time `.startOf(unit: string)`

Returns a cloned `Dayjs` set to the start of the specified unit of time.

```js
dayjs().startOf('week');
```

### End of Time `.endOf(unit: string)`

Returns a cloned `Dayjs` set to the end of the specified unit of time.

```js
dayjs().endOf('month');
```

## Displaying

### Format `.format(stringWithTokens: string)`

Returns a `string` with the `Dayjs`'s formatted date.
To escape characters, wrap them in square or culy brackets (e.g. `[G] {um}`).

```js
dayjs().format(); // current date in ISO6801, without fraction seconds e.g. '2020-04-02T08:02:17-05:00'

dayjs('2019-01-25').format('{YYYY} MM-DDTHH:mm:ssZ[Z]'); // '{2019} 01-25T00:00:00-02:00Z'

dayjs('2019-01-25').format('DD/MM/YYYY'); // '25/01/2019'
```

#### List of all available formats

| Format | Output           | Description                           |
| ------ | ---------------- | ------------------------------------- |
| `YY`   | 18               | Two-digit year                        |
| `YYYY` | 2018             | Four-digit year                       |
| `M`    | 1-12             | The month, beginning at 1             |
| `MM`   | 01-12            | The month, 2-digits                   |
| `MMM`  | Jan-Dec          | The abbreviated month name            |
| `MMMM` | January-December | The full month name                   |
| `D`    | 1-31             | The day of the month                  |
| `DD`   | 01-31            | The day of the month, 2-digits        |
| `d`    | 0-6              | The day of the week, with Sunday as 0 |
| `dddd` | Sunday-Saturday  | The name of the day of the week       |
| `H`    | 0-23             | The hour                              |
| `HH`   | 00-23            | The hour, 2-digits                    |
| `h`    | 1-12             | The hour, 12-hour clock               |
| `hh`   | 01-12            | The hour, 12-hour clock, 2-digits     |
| `m`    | 0-59             | The minute                            |
| `mm`   | 00-59            | The minute, 2-digits                  |
| `s`    | 0-59             | The second                            |
| `ss`   | 00-59            | The second, 2-digits                  |
| `SSS`  | 000-999          | The millisecond, 3-digits             |
| `Z`    | +5:00            | The offset from UTC                   |
| `ZZ`   | +0500            | The offset from UTC, 2-digits         |
| `A`    | AM PM            |                                       |
| `a`    | am pm            |                                       |

* More available formats `Q Do k kk X x ...` in plugin [`AdvancedFormat`](./Plugin.md#advancedformat)

### Difference `.diff(compared: Dayjs, unit: string (default: 'milliseconds'), float?: boolean)`

Returns a `number` indicating the difference of two `Dayjs`s in the specified unit.

```js
const date1 = dayjs('2019-01-25');
const date2 = dayjs('2018-06-05');
date1.diff(date2); // 20214000000
date1.diff(date2, 'months'); // 7
date1.diff(date2, 'months', true); // 7.645161290322581
date1.diff(date2, 'days'); // 233
```

### Unix Timestamp (milliseconds) `.valueOf()`

Returns the `number` of milliseconds since the Unix Epoch for the `Dayjs`.

```js
dayjs('2019-01-25').valueOf(); // 1548381600000
```

### Unix Timestamp (seconds) `.unix()`

Returns the `number` of seconds since the Unix Epoch for the `Dayjs`.

```js
dayjs('2019-01-25').unix(); // 1548381600
```

### Days in the Month `.daysInMonth()`

Returns the `number` of days in the `Dayjs`'s month.

```js
dayjs('2019-01-25').daysInMonth(); // 31
```

### As Javascript Date `.toDate()`

Returns a copy of the native `Date` object parsed from the `Dayjs` object.

```js
dayjs('2019-01-25').toDate();
```

### As Array `.toArray()`

Returns an `array` that mirrors the parameters from new Date().

```js
dayjs('2019-01-25').toArray(); // [ 2019, 0, 25, 0, 0, 0, 0 ]
```

### As JSON `.toJSON()`

Returns the `Dayjs` formatted in an ISO8601 `string`.

```js
dayjs('2019-01-25').toJSON(); // '2019-01-25T02:00:00.000Z'
```

### As ISO 8601 String `.toISOString()`

Returns the `Dayjs` formatted in an ISO8601 `string`.

```js
dayjs('2019-01-25').toISOString(); // '2019-01-25T02:00:00.000Z'
```

### As Object `.toObject()`

Returns an `object` with the date's properties.

```js
dayjs('2019-01-25').toObject();
/* { years: 2019,
     months: 0,
     date: 25,
     hours: 0,
     minutes: 0,
     seconds: 0,
     milliseconds: 0 } */
```

### As String `.toString()`

Returns a `string` representation of the date.

```js
dayjs('2019-01-25').toString(); // 'Fri, 25 Jan 2019 02:00:00 GMT'
```

## Query

### Is Before `.isBefore(compared: Dayjs)`

Returns a `boolean` indicating whether the `Dayjs`'s date is before the other supplied `Dayjs`'s.

```js
dayjs().isBefore(dayjs()); // false
```

### Is Same `.isSame(compared: Dayjs)`

Returns a `boolean` indicating whether the `Dayjs`'s date is the same as the other supplied `Dayjs`'s.

```js
dayjs().isSame(dayjs()); // true
```

### Is After `.isAfter(compared: Dayjs)`

Returns a `boolean` indicating whether the `Dayjs`'s date is after the other supplied `Dayjs`'s.

```js
dayjs().isAfter(dayjs()); // false
```

### Is Leap Year `.isLeapYear()`

Returns a `boolean` indicating whether the `Dayjs`'s year is a leap year or not.

```js
dayjs('2000-01-01').isLeapYear(); // true
```

## Plugin APIs

### RelativeTime

`.from` `.to` `.fromNow` `.toNow` to get relative time

plugin [`RelativeTime`](./Plugin.md#relativetime)
