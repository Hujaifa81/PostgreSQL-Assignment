
## ❓ প্রশ্ন: Explain the Primary Key and Foreign Key concepts in PostgreSQL.

### 🔹 Primary Key:
**Primary Key** হলো একটি কলাম (বা কলামসমষ্টি) যা একটি টেবিলের প্রতিটি রেকর্ডকে অন্য রেকর্ড থেকে স্বতন্ত্রভাবে চিহ্নিত করতে সাহায্য করে। এটি **null হতে পারে না** এবং **ডুপ্লিকেট মান থাকতে পারে না**।

#### ✅ বৈশিষ্ট্য:
1. এক টেবিলে শুধুমাত্র একটি Primary Key থাকতে পারে।
2. Primary Key-এর মান অন্য কোনো রেকর্ডের সাথে মিলতে পারে না।

---

### 🔹 Foreign Key:
**Foreign Key** হলো এমন একটি কলাম (বা কলামসমষ্টি) যা অন্য টেবিলের Primary Key-এর সাথে সম্পর্ক স্থাপন করে। এটি দুটি টেবিলের মধ্যে রিলেশন বা সংযোগ স্থাপন করে এবং **ডেটার অখণ্ডতা (data integrity)** নিশ্চিত করে।

#### ✅ বৈশিষ্ট্য:
1. এটি একটি টেবিলের একটি কলাম হয়, যা অন্য টেবিলের Primary Key-এর সাথে সম্পর্কিত।
2. এটি নিশ্চিত করে যে, যে মানটি Foreign Key-তে রাখা হয়েছে, তা অবশ্যই মূল (parent) টেবিলে আগে থেকে থাকতে হবে।
3. এটি Parent-Child সম্পর্ক বোঝায়।

---

### 🎯 গুরুত্ব:
- Primary Key নিশ্চিত করে যে আমাদের ডেটাবেসে কোনো ডুপ্লিকেট রেকর্ড নেই।
- Foreign Key নিশ্চিত করে যে টেবিলগুলোর মধ্যে সম্পর্ক থাকে এবং ডেটা বিভ্রান্ত হয় না।
- এটি ডেটাবেজ **normalization**-এ গুরুত্বপূর্ণ ভূমিকা রাখে।
- Data Integrity ও Referential Integrity বজায় থাকে।

---

## ❓ প্রশ্ন: What is the difference between the VARCHAR and CHAR data types?

### 🔸 CHAR(n) (Fixed-length Character):
1. **CHAR** একটি **স্থির দৈর্ঘ্যের (fixed-length)** ডেটা টাইপ।
2. যদি `CHAR(10)` হয় এবং আপনি "HELLO" দেন, তাহলে PostgreSQL এটিকে ১০টি ক্যারেক্টারে রূপান্তর করবে, অর্থাৎ বাকি ৫টি জায়গায় স্পেস ভরে দেবে।

### 🔸 VARCHAR(n) (Variable-length Character):
1. **VARCHAR** একটি **পরিবর্তনশীল দৈর্ঘ্যের (variable-length)** ডেটা টাইপ।
2. `VARCHAR(10)` হলে সর্বোচ্চ ১০টি অক্ষর রাখা যাবে, কিন্তু কম হলে সমস্যা নেই।
3. এটি প্রয়োজন অনুযায়ী স্পেস ব্যবহার করে, অপ্রয়োজনীয় জায়গা নষ্ট করে না।

---

## ❓ প্রশ্ন: Explain the purpose of the WHERE clause in a SELECT statement.

**WHERE clause** হলো একটি শর্ত, যা SELECT, UPDATE, DELETE ইত্যাদি SQL স্টেটমেন্টের সাথে ব্যবহার করা হয়। এটি রেকর্ড **ফিল্টার** করার জন্য ব্যবহৃত হয়।

### ✅ উদ্দেশ্য:
1. **নির্দিষ্ট ডেটা** খুঁজে বের করা যায়।
2. **পারফরম্যান্স উন্নত** হয় কারণ কম ডেটা রিট্রিভ হয়।
3. **ডেটা নিরাপত্তা** নিশ্চিত হয় — শুধু প্রয়োজনীয় তথ্য দেখানো যায়।
4. AND, OR, NOT, LIKE, BETWEEN, IN ইত্যাদি **লজিক্যাল অপারেটর** ব্যবহার করা যায়।

### 🔍 উদাহরণ:
```sql
SELECT *
FROM employees
WHERE department = 'HR' AND salary > 30000;

SELECT name
FROM customers
WHERE name LIKE 'A%';
```
---

## ❓ প্রশ্ন: What is the significance of the JOIN operation, and how does it work in PostgreSQL?

**JOIN** হলো একটি SQL অপারেশন যার মাধ্যমে আমরা একাধিক টেবিলের মধ্যে সম্পর্ক তৈরি করে তাদের ডেটা একসাথে বের করতে পারি। এটি মূলত টেবিলগুলোর মধ্যে সম্পর্কিত কলামগুলো ব্যবহার করে কাজ করে।

### 🔍 PostgreSQL (এবং অন্যান্য রিলেশনাল ডেটাবেজেও) JOIN ব্যবহারের উদ্দেশ্য:

1. বিভিন্ন টেবিলের **কম্বাইন্ড (combined)** ডেটা দেখা  
2. **রিপোর্ট** তৈরি করা  
3. **ডেটা বিশ্লেষণ (analysis)** করা

### 🤔 JOIN কেন দরকার?

আমরা সাধারণত ডেটাবেজ ডিজাইন করি **নরমালাইজড আকারে**, অর্থাৎ, ডেটা টুকরো টুকরো করে আলাদা টেবিলে রাখি ডুপ্লিকেট এড়ানোর জন্য। কিন্তু যখন সেগুলো একসাথে দরকার হয়, তখনই JOIN ব্যবহার করি।

---

### 🧩 JOIN এর ধরণ ও কাজ:

| JOIN ধরন         | কাজের বিবরণ |
|------------------|--------------|
| **INNER JOIN**   | শুধু মিল পাওয়া রেকর্ডগুলো দেখায় |
| **LEFT JOIN**    | বাম টেবিলের সব রেকর্ড, আর ডান টেবিলের মিল থাকলে সেই মান দেয়, না থাকলে `NULL` |
| **RIGHT JOIN**   | ডান টেবিলের সব রেকর্ড, বাম টেবিলের মিল থাকলে দেয়, না থাকলে `NULL` |
| **FULL OUTER JOIN** | দুই টেবিলের সব রেকর্ড, যেখানে মিল নেই সেখানে `NULL` |
| **CROSS JOIN**   | প্রতিটি রেকর্ড একে অপরের সাথে মিলায় — **কার্টেশিয়ান প্রোডাক্ট** |

---

### 🧪 উদাহরণ: INNER JOIN 
```sql
SELECT s.name, c.course_name
FROM students s
INNER JOIN courses c
ON s.student_id = c.student_id;
```
### 🧪 উদাহরণ: LEFT JOIN
```sql
SELECT s.name, c.course_name
FROM students s
LEFT JOIN courses c
ON s.student_id = c.student_id;
```
---

## ❓ প্রশ্ন: Explain the GROUP BY clause and its role in aggregation operations

**GROUP BY** হলো SQL-এর একটি clause, যা ডেটাকে নির্দিষ্ট একটি বা একাধিক কলামের উপর ভিত্তি করে গোষ্ঠীভুক্ত (group) করে এবং প্রতিটি গ্রুপের উপর অ্যাগ্রিগেট ফাংশন (SUM, COUNT, AVG, MAX, MIN ইত্যাদি) প্রয়োগ করে।

### উদ্দেশ্য:
1. ডেটাকে বিভাগভিত্তিক বিভাজন করে।  
2. প্রতি গ্রুপের উপর গাণিতিক হিসাব করতে দেয়।  
3. রিপোর্টিং এবং ডেটা বিশ্লেষণ সহজ করে।  

### GROUP BY এর সাথে ব্যবহৃত Aggregation Functions:

| Function | কাজ                        |
| -------- | -------------------------- |
| SUM()    | সংখ্যাগুলোর যোগফল          |
| AVG()    | গড় হিসাব করে              |
| COUNT()  | কতটি রেকর্ড আছে গুনে      |
| MAX()    | সর্বোচ্চ মান               |
| MIN()    | সর্বনিম্ন মান              |

### GROUP BY এর গঠন (Syntax):

```sql
SELECT column_name, AGGREGATE_FUNCTION(column_name)
FROM table_name
GROUP BY column_name;
```
```sql
SELECT class, AVG(marks) AS avg_marks
FROM students
GROUP BY class;
```





