# Faker Command Line Tool

[Faker](https://github.com/fzaninotto/faker) is a PHP library that generates fake data for you.
This is a command line tool for easy generation of fake data in a static way. 

## Basic Usage

Use `bin/faker.php` to generate fake data on the command line.

```
$ ./bin/faker.php --count 10 word

[
    "culpa",
    "consequatur",
    "quisquam",
    "recusandae",
    "asperiores",
    "accusamus",
    "nihil",
    "repellat",
    "vero",
    "omnis"
]
```

You can use different output formats by definint the `--format` option. JSON is the default format.

### XML output

```
$ ./bin/faker.php --format xml --count 10 word

<?xml version="1.0"?>
<array>
  <item>culpa</item>
  <item>consequatur</item>
  <item>quisquam</item>
  <item>recusandae</item>
  <item>asperiores</item>
  <item>accusamus</item>
  <item>nihil</item>
  <item>repellat</item>
  <item>vero</item>
  <item>omnis</item>
</array>
```

### CSV output

```
$ ./bin/faker.php --format csv --count 10 word

culpa
consequatur
quisquam
recusandae
asperiores
accusamus
nihil
repellat
vero
omnis
```

### PHP output

```
$ ./bin/faker.php --format php --count 10 word

array (
  0 => 'culpa',
  1 => 'consequatur',
  2 => 'quisquam',
  3 => 'recusandae',
  4 => 'asperiores',
  5 => 'accusamus',
  6 => 'nihil',
  7 => 'repellat',
  8 => 'vero',
  9 => 'omnis',
)
```

### printf and vprintf output

The printf and vprintf output are mostly equal. But `printf` is designed for single value generator types e.g. `safeEmail` and `vprintf` is designed for multi value generator types e.g. `words 5`.

```
$ ./bin/faker.php --format printf \
  --pattern "INSERT INTO emails (uuid, email) VALUES (UUID(), %s);" \
  --enclosure "'" \
  --count 10 safeEmail
  
INSERT INTO emails (uuid, email) VALUES (UUID(), 'dbednar@example.com');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'xhettinger@example.net');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'gerald62@example.org');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'miles91@example.com');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'to\'conner@example.com');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'bridgette.runolfsdottir@example.com');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'fgoldner@example.org');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'grimes.leo@example.org');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'lilian.reynolds@example.net');
INSERT INTO emails (uuid, email) VALUES (UUID(), 'ratke.darlene@example.net');
```

```
./bin/faker.php --format vprintf \
  --pattern "INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), %s, %s, %s);" \
  --enclosure "'" \
  --count 10 words 3
  
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'est', 'illo', 'consequuntur');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'dolorem', 'temporibus', 'commodi');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'sint', 'reiciendis', 'sint');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'sunt', 'eum', 'id');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'tempora', 'rerum', 'occaecati');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'corrupti', 'impedit', 'doloribus');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'amet', 'consectetur', 'repudiandae');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'est', 'id', 'amet');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'odio', 'facere', 'nesciunt');
INSERT INTO keywords (uuid, keyword1, keyword2, keyword3) VALUES (UUID(), 'voluptas', 'quia', 'rerum');
```

You can also use `printf` with multi value generator types, which will joined by the `--delimiter` char, which is `,` by default.

```
$ ./bin/faker.php --format printf \
  --pattern "INSERT INTO words (uuid, words) VALUES (UUID(), %s);" \
  --delimiter ', ' \
  --enclosure "'" \
  --count 10 words 10

INSERT INTO words (uuid, words) VALUES (UUID(), 'est, illo, consequuntur, dolorem, temporibus, commodi, sint, reiciendis, sint, sunt');
INSERT INTO words (uuid, words) VALUES (UUID(), 'eum, id, tempora, rerum, occaecati, corrupti, impedit, doloribus, amet, consectetur');
INSERT INTO words (uuid, words) VALUES (UUID(), 'repudiandae, est, id, amet, odio, facere, nesciunt, voluptas, quia, rerum');
INSERT INTO words (uuid, words) VALUES (UUID(), 'ad, sed, esse, sed, exercitationem, sed, et, rem, esse, excepturi');
INSERT INTO words (uuid, words) VALUES (UUID(), 'animi, minus, qui, perferendis, quo, repudiandae, aliquam, dolorem, voluptas, fugiat');
INSERT INTO words (uuid, words) VALUES (UUID(), 'at, odit, dolorem, a, aperiam, dignissimos, ipsa, sunt, consequatur, alias');
INSERT INTO words (uuid, words) VALUES (UUID(), 'accusantium, voluptatum, autem, nobis, cumque, neque, modi, iure, voluptatem, error');
INSERT INTO words (uuid, words) VALUES (UUID(), 'molestiae, consequatur, alias, eligendi, corrupti, illum, commodi, molestiae, aut, repellat');
INSERT INTO words (uuid, words) VALUES (UUID(), 'id, quisquam, et, sit, consequuntur, aut, et, ullam, asperiores, molestiae');
INSERT INTO words (uuid, words) VALUES (UUID(), 'cupiditate, culpa, voluptatem, et, mollitia, dolor, sit, nisi, praesentium, qui');
```

It is recommend to use the `--enclosure` option. each occurrence of the `--enclosure` char will be escaped with the `--escape` char, which is `\\` by default.

## License

Faker Command Line Tool is released under the MIT Licence. See the bundled LICENSE file for details.