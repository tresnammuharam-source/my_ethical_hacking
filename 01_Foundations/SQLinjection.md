# SQL Injection

website yang membutuhkan credential atau user dan password ini rentan untuk dilakukan sql injection jika input pada credential tidak di sanitasi.
dengan menggunakan user name acah, lanutnya password dibuat memeprcayai defifinisi yng mereka buat sendiri dan ditambahkan or sepeerti `password : 'abc' or 1=1;-- -

> SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';

