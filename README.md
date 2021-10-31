# [SQL練習問題 – 一覧まとめ](https://tech.pjin.jp/blog/2016/12/05/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E4%B8%80%E8%A6%A7%E3%81%BE%E3%81%A8%E3%82%81/)

```
https://tech.pjin.jp/blog/2016/04/30/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E5%95%8F1/
mysql> select c.group_name, min(c.ranking), max(c.ranking) from countries as c group by c.group_name;
+------------+----------------+----------------+
| group_name | min(c.ranking) | max(c.ranking) |
+------------+----------------+----------------+
| A          |              3 |             56 |
| B          |              1 |             62 |
| C          |              8 |             46 |
| D          |              7 |             28 |
| E          |              6 |             33 |
| F          |              5 |             44 |
| G          |              2 |             37 |
| H          |             11 |             57 |
+------------+----------------+----------------+
8 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/04/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f2/
mysql> select avg(height) as 平均身長, avg(weight) as 平均体重 from players where position = 'GK';
+--------------+--------------+
| 平均身長     | 平均体重     |
+--------------+--------------+
|     187.6250 |      82.8854 |
+--------------+--------------+
1 row in set (0.01 sec)


https://tech.pjin.jp/blog/2016/04/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f3/
mysql> select c.name, avg(p.height) from countries as c right join players as p on c.id = p.country_id group by c.id, c.name order by avg(p.height) desc;
+--------------------------------------+---------------+
| name                                 | avg(p.height) |
+--------------------------------------+---------------+
| ドイツ                               |      185.7391 |
| ベルギー                             |      185.1739 |
| ボスニア・ヘルツェゴビナ             |      184.9130 |
| ギリシャ                             |      184.6087 |
| クロアチア                           |      183.8261 |
| 韓国                                 |      183.8261 |
| イングランド                         |      183.6087 |
| 米国                                 |      183.2174 |
| アルジェリア                         |      183.1739 |
| ナイジェリア                         |      183.0870 |
| スイス                               |      182.8696 |
| イタリア                             |      182.8261 |
| イラン                               |      182.4348 |
| ロシア                               |      181.8261 |
| ポルトガル                           |      181.7826 |
| オーストラリア                       |      181.6522 |
| アルゼンチン                         |      181.6087 |
| カメルーン                           |      181.3478 |


https://tech.pjin.jp/blog/2016/04/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f4/
mysql> select (select c.name from countries as c where c.id = p.country_id) as name, avg(p.height) from players as p group by p.country_id order by avg(p.height) desc;
+--------------------------------------+---------------+
| name                                 | avg(p.height) |
+--------------------------------------+---------------+
| ドイツ                               |      185.7391 |
| ベルギー                             |      185.1739 |
| ボスニア・ヘルツェゴビナ             |      184.9130 |
| ギリシャ                             |      184.6087 |
| クロアチア                           |      183.8261 |
| 韓国                                 |      183.8261 |
| イングランド                         |      183.6087 |
| 米国                                 |      183.2174 |
| アルジェリア                         |      183.1739 |
| ナイジェリア                         |      183.0870 |
| スイス                               |      182.8696 |
| イタリア                             |      182.8261 |
| イラン                               |      182.4348 |
| ロシア                               |      181.8261 |
| ポルトガル                           |      181.7826 |
| オーストラリア                       |      181.6522 |


https://tech.pjin.jp/blog/2016/05/12/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f5/
mysql> select p.kickoff, c.name, ec.name from pairings as p join countries as c on p.my_country_id = c.id join countries as ec on p.enemy_country_id = ec.id order by p.kickoff asc;
+---------------------+--------------------------------------+--------------------------------------+
| kickoff             | name                                 | name                                 |
+---------------------+--------------------------------------+--------------------------------------+
| 2014-06-13 05:00:00 | ブラジル                             | クロアチア                           |
| 2014-06-13 05:00:00 | クロアチア                           | ブラジル                             |
| 2014-06-14 01:00:00 | カメルーン                           | メキシコ                             |
| 2014-06-14 01:00:00 | メキシコ                             | カメルーン                           |
| 2014-06-14 04:00:00 | オランダ                             | スペイン                             |
| 2014-06-14 04:00:00 | スペイン                             | オランダ                             |
| 2014-06-14 07:00:00 | オーストラリア                       | チリ                                 |
| 2014-06-14 07:00:00 | チリ                                 | オーストラリア                       |
| 2014-06-15 01:00:00 | コロンビア                           | ギリシャ                             |
| 2014-06-15 01:00:00 | ギリシャ                             | コロンビア                           |
| 2014-06-15 04:00:00 | コスタリカ                           | ウルグアイ                           |
| 2014-06-15 04:00:00 | ウルグアイ                           | コスタリカ                           |
| 2014-06-15 07:00:00 | イタリア                             | イングランド                         |
| 2014-06-15 07:00:00 | イングランド                         | イタリア                             |


https://tech.pjin.jp/blog/2016/05/12/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f6/
mysql> select p.name, p.position, p.club, (select count(g.id) from goals as g where p.id = g.player_id) as point from players as p order by point desc limit 10;
+-----------------------+----------+------------------------------------------------+-------+
| name                  | position | club                                           | point |
+-----------------------+----------+------------------------------------------------+-------+
| ロドリゲス            | MF       | モナコ（フランス）                             |     7 |
| ミュラー              | MF       | Bミュンヘン                                    |     6 |
| ファンペルシー        | FW       | マンチェスターU（イングランド）                |     5 |
| シュルレ              | MF       | チェルシー（イングランド）                     |     5 |
| クロース              | MF       | Bミュンヘン                                    |     4 |
| メッシ                | FW       | バルセロナ（スペイン）                         |     4 |
| ネイマール            | FW       | バルセロナ（スペイン）                         |     4 |
| クローゼ              | FW       | ラツィオ（イタリア）                           |     3 |
| シャキリ              | MF       | Bミュンヘン（ドイツ）                          |     3 |
| ベンゼマ              | FW       | Rマドリード（スペイン）                        |     3 |
+-----------------------+----------+------------------------------------------------+-------+
10 rows in set (0.04 sec)


https://tech.pjin.jp/blog/2016/05/12/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f7/
mysql> select p.name, p.position, p.club, count(g.id) as point from players as p left join goals as g on p.id = g.player_id group by p.id, p.name, p.position, p.club order by point desc;
+--------------------------------------+----------+--------------------------------------------------------------------+-------+
| name                                 | position | club                                                               | point |
+--------------------------------------+----------+--------------------------------------------------------------------+-------+
| ロドリゲス                           | MF       | モナコ（フランス）                                                 |     7 |
| ミュラー                             | MF       | Bミュンヘン                                                        |     6 |
| シュルレ                             | MF       | チェルシー（イングランド）                                         |     5 |
| ファンペルシー                       | FW       | マンチェスターU（イングランド）                                    |     5 |
| クロース                             | MF       | Bミュンヘン                                                        |     4 |
| メッシ                               | FW       | バルセロナ（スペイン）                                             |     4 |
| ネイマール                           | FW       | バルセロナ（スペイン）                                             |     4 |
| シャキリ                             | MF       | Bミュンヘン（ドイツ）                                              |     3 |
| E・バレンシア                        | FW       | パチューカ（メキシコ）                                             |     3 |
| ベンゼマ                             | FW       | Rマドリード（スペイン）                                            |     3 |
| ロッベン                             | MF       | Bミュンヘン（ドイツ）                                              |     3 |
| サンチェス                           | FW       | バルセロナ（スペイン）                                             |     3 |
| ジャブ                               | MF       | クラブ・アフリカン（チュニジア）                                   |     3 |
| クローゼ                             | FW       | ラツィオ（イタリア）                                               |     3 |
| フンメルス                           | DF       | ドルトムント                                                       |     3 |
| パパスタソプロス                     | DF       | ドルトムント（ドイツ）                                             |     2 |
| デパイ                               | FW       | PSV                                                                |     2 |
| スアレス                             | FW       | リバプール（イングランド）                                         |     2 |


https://tech.pjin.jp/blog/2016/05/12/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f8/
mysql> select p.position, count(g.id) as point from players as p join goals as g on p.id = g.player_id group by p.position order by point desc;
+----------+-------+
| position | point |
+----------+-------+
| FW       |    91 |
| MF       |    72 |
| DF       |    20 |
+----------+-------+
3 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2016/06/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f9/
mysql> select p.birth, timestampdiff(year, p.birth, str_to_date('2014-06-13', '%Y-%m-%d')) as age, p.name, p.position from players as p order by age desc limit 10;
+------------+------+-----------------------+----------+
| birth      | age  | name                  | position |
+------------+------+-----------------------+----------+
| 1971-06-21 |   42 | モンドラゴン          | GK       |
| 1976-01-13 |   38 | ジェペス              | DF       |
| 1977-03-06 |   37 | カラグニス            | MF       |
| 1977-05-03 |   37 | バジャダレス          | GK       |
| 1978-06-09 |   36 | クローゼ              | FW       |
| 1978-01-28 |   36 | ブフォン              | GK       |
| 1978-03-11 |   36 | ドログバ              | FW       |
| 1978-02-07 |   36 | バンビュイテン        | DF       |
| 1979-01-08 |   35 | プレティコサ          | GK       |
| 1979-05-19 |   35 | ピルロ                | MF       |
+------------+------+-----------------------+----------+
10 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2016/06/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f10/
mysql> select count(id) from goals where player_id is null;
+-----------+
| count(id) |
+-----------+
|         5 |
+-----------+
1 row in set (0.01 sec)


https://tech.pjin.jp/blog/2016/06/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f11/
mysql> select c.group_name, count(g.id) from goals as g join pairings as p on g.pairing_id = p.id join countries as c on p.my_country_id = c.id where p.kickoff between '2014-06-13 00:00:00' and '2014-06-27 23:59:59' group by c.group_name;
+------------+-------------+
| group_name | count(g.id) |
+------------+-------------+
| A          |          18 |
| B          |          22 |
| C          |          17 |
| D          |          12 |
| E          |          19 |
| F          |          14 |
| G          |          19 |
| H          |          15 |
+------------+-------------+
8 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2016/06/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f12/
mysql> select g.goal_time from goals as g join pairings as p on g.pairing_id = p.id join players as pl on g.player_id = pl.id join countries as c on pl.country_id = c.id where p.id = 103 and c.id = 9;
+-------------+
| goal_time   |
+-------------+
| 前半17分    |
| 後半45分    |
| 後半10分    |
| 後半37分    |
+-------------+
4 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/07/15/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f13/
mysql> select c.name, count(g.id) from goals as g join pairings as p on g.pairing_id = p.id join countries as c on p.my_country_id = c.id where p.id in (39, 103) group by c.id;
+-----------------+-------------+
| name            | count(g.id) |
+-----------------+-------------+
| コロンビア      |           4 |
| 日本            |           1 |
+-----------------+-------------+
2 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/07/19/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f14/
mysql> select p.kickoff, c.name, ec.name, c.ranking, ec.ranking, count(g.id) from pairings as p left outer join countries as c on p.my_country_id = c.id left outer join countries as ec on p.enemy_country_id = ec.id left outer join goals as g on p.id = g.pairing_id where c.group_name = 'C' and ec.group_name = 'C' group by p.kickoff, c.name, ec.name, c.ranking, ec.ranking order by p.kickoff asc, c.ranking asc;
+---------------------+--------------------------+--------------------------+---------+---------+-------------+
| kickoff             | name                     | name                     | ranking | ranking | count(g.id) |
+---------------------+--------------------------+--------------------------+---------+---------+-------------+
| 2014-06-15 01:00:00 | コロンビア               | ギリシャ                 |       8 |      12 |           3 |
| 2014-06-15 01:00:00 | ギリシャ                 | コロンビア               |      12 |       8 |           0 |
| 2014-06-15 10:00:00 | コートジボワール         | 日本                     |      23 |      46 |           2 |
| 2014-06-15 10:00:00 | 日本                     | コートジボワール         |      46 |      23 |           1 |
| 2014-06-20 01:00:00 | コロンビア               | コートジボワール         |       8 |      23 |           2 |
| 2014-06-20 01:00:00 | コートジボワール         | コロンビア               |      23 |       8 |           1 |
| 2014-06-20 07:00:00 | ギリシャ                 | 日本                     |      12 |      46 |           0 |
| 2014-06-20 07:00:00 | 日本                     | ギリシャ                 |      46 |      12 |           0 |
| 2014-06-25 05:00:00 | コロンビア               | 日本                     |       8 |      46 |           4 |
| 2014-06-25 05:00:00 | ギリシャ                 | コートジボワール         |      12 |      23 |           2 |
| 2014-06-25 05:00:00 | コートジボワール         | ギリシャ                 |      23 |      12 |           1 |
| 2014-06-25 05:00:00 | 日本                     | コロンビア               |      46 |       8 |           1 |
+---------------------+--------------------------+--------------------------+---------+---------+-------------+
12 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/07/21/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f15/
mysql> select p.kickoff, c.name, ec.name, c.ranking, ec.ranking, (select count(g.id) from goals as g where p.id = g.pairing_id) as point from pairings as p left outer join countries as c on p.my_country_id = c.id left outer join countries as ec on p.enemy_country_id = ec.id where c.group_name = 'C' and ec.group_name = 'C' order by p.kickoff asc, c.ranking asc;
+---------------------+--------------------------+--------------------------+---------+---------+-------+
| kickoff             | name                     | name                     | ranking | ranking | point |
+---------------------+--------------------------+--------------------------+---------+---------+-------+
| 2014-06-15 01:00:00 | コロンビア               | ギリシャ                 |       8 |      12 |     3 |
| 2014-06-15 01:00:00 | ギリシャ                 | コロンビア               |      12 |       8 |     0 |
| 2014-06-15 10:00:00 | コートジボワール         | 日本                     |      23 |      46 |     2 |
| 2014-06-15 10:00:00 | 日本                     | コートジボワール         |      46 |      23 |     1 |
| 2014-06-20 01:00:00 | コロンビア               | コートジボワール         |       8 |      23 |     2 |
| 2014-06-20 01:00:00 | コートジボワール         | コロンビア               |      23 |       8 |     1 |
| 2014-06-20 07:00:00 | ギリシャ                 | 日本                     |      12 |      46 |     0 |
| 2014-06-20 07:00:00 | 日本                     | ギリシャ                 |      46 |      12 |     0 |
| 2014-06-25 05:00:00 | コロンビア               | 日本                     |       8 |      46 |     4 |
| 2014-06-25 05:00:00 | ギリシャ                 | コートジボワール         |      12 |      23 |     2 |
| 2014-06-25 05:00:00 | コートジボワール         | ギリシャ                 |      23 |      12 |     1 |
| 2014-06-25 05:00:00 | 日本                     | コロンビア               |      46 |       8 |     1 |
+---------------------+--------------------------+--------------------------+---------+---------+-------+
12 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/07/25/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f16/
mysql> select p.kickoff, c.name, ec.name, c.ranking, ec.ranking, (select count(g.id) from goals as g where p.id = g.pairing_id) as point, (select count(eg.id) from goals as eg join pairings as ep on eg.pairing_id = ep.id where p.my_country_id = ep.enemy_country_id and p.enemy_country_id = ep.my_country_id) as epoint from pairings as p left outer join countries as c on p.my_country_id = c.id left outer join countries as ec on p.enemy_country_id = ec.id where c.group_name = 'C' and ec.group_name = 'C' order by p.kickoff asc, c.ranking asc;
+---------------------+--------------------------+--------------------------+---------+---------+-------+--------+
| kickoff             | name                     | name                     | ranking | ranking | point | epoint |
+---------------------+--------------------------+--------------------------+---------+---------+-------+--------+
| 2014-06-15 01:00:00 | コロンビア               | ギリシャ                 |       8 |      12 |     3 |      0 |
| 2014-06-15 01:00:00 | ギリシャ                 | コロンビア               |      12 |       8 |     0 |      3 |
| 2014-06-15 10:00:00 | コートジボワール         | 日本                     |      23 |      46 |     2 |      1 |
| 2014-06-15 10:00:00 | 日本                     | コートジボワール         |      46 |      23 |     1 |      2 |
| 2014-06-20 01:00:00 | コロンビア               | コートジボワール         |       8 |      23 |     2 |      1 |
| 2014-06-20 01:00:00 | コートジボワール         | コロンビア               |      23 |       8 |     1 |      2 |
| 2014-06-20 07:00:00 | ギリシャ                 | 日本                     |      12 |      46 |     0 |      0 |
| 2014-06-20 07:00:00 | 日本                     | ギリシャ                 |      46 |      12 |     0 |      0 |
| 2014-06-25 05:00:00 | コロンビア               | 日本                     |       8 |      46 |     4 |      1 |
| 2014-06-25 05:00:00 | ギリシャ                 | コートジボワール         |      12 |      23 |     2 |      1 |
| 2014-06-25 05:00:00 | コートジボワール         | ギリシャ                 |      23 |      12 |     1 |      2 |
| 2014-06-25 05:00:00 | 日本                     | コロンビア               |      46 |       8 |     1 |      4 |
+---------------------+--------------------------+--------------------------+---------+---------+-------+--------+
12 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/08/26/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f17/
mysql> select p.kickoff, c.name, ec.name, c.ranking, ec.ranking, (select count(g.id) from goals as g where p.id = g.pairing_id) as point, (select count(eg.id) from goals as eg join pairings as ep on eg.pairing_id = ep.id where p.my_country_id = ep.enemy_country_id and p.enemy_country_id = ep.my_country_id) as epoint, ((select count(g.id) from goals as g where p.id = g.pairing_id) - (select count(eg.id) from goals as eg join pairings as ep on eg.pairing_id = ep.id where p.my_country_id = ep.enemy_country_id and p.enemy_country_id = ep.my_country_id)) as point_diff from pairings as p left outer join countries as c on p.my_country_id = c.id left outer join countries as ec on p.enemy_country_id = ec.id where c.group_name = 'C' and ec.group_name = 'C' order by p.kickoff asc, c.ranking asc;
+---------------------+--------------------------+--------------------------+---------+---------+-------+--------+------------+
| kickoff             | name                     | name                     | ranking | ranking | point | epoint | point_diff |
+---------------------+--------------------------+--------------------------+---------+---------+-------+--------+------------+
| 2014-06-15 01:00:00 | コロンビア               | ギリシャ                 |       8 |      12 |     3 |      0 |          3 |
| 2014-06-15 01:00:00 | ギリシャ                 | コロンビア               |      12 |       8 |     0 |      3 |         -3 |
| 2014-06-15 10:00:00 | コートジボワール         | 日本                     |      23 |      46 |     2 |      1 |          1 |
| 2014-06-15 10:00:00 | 日本                     | コートジボワール         |      46 |      23 |     1 |      2 |         -1 |
| 2014-06-20 01:00:00 | コロンビア               | コートジボワール         |       8 |      23 |     2 |      1 |          1 |
| 2014-06-20 01:00:00 | コートジボワール         | コロンビア               |      23 |       8 |     1 |      2 |         -1 |
| 2014-06-20 07:00:00 | ギリシャ                 | 日本                     |      12 |      46 |     0 |      0 |          0 |
| 2014-06-20 07:00:00 | 日本                     | ギリシャ                 |      46 |      12 |     0 |      0 |          0 |
| 2014-06-25 05:00:00 | コロンビア               | 日本                     |       8 |      46 |     4 |      1 |          3 |
| 2014-06-25 05:00:00 | ギリシャ                 | コートジボワール         |      12 |      23 |     2 |      1 |          1 |
| 2014-06-25 05:00:00 | コートジボワール         | ギリシャ                 |      23 |      12 |     1 |      2 |         -1 |
| 2014-06-25 05:00:00 | 日本                     | コロンビア               |      46 |       8 |     1 |      4 |         -3 |
+---------------------+--------------------------+--------------------------+---------+---------+-------+--------+------------+
12 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/08/26/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f18/
mysql> select p.kickoff, date_add(p.kickoff, interval -12 hour) from pairings as p where p.my_country_id = 1 and p.enemy_country_id = 4;
+---------------------+----------------------------------------+
| kickoff             | date_add(p.kickoff, interval -12 hour) |
+---------------------+----------------------------------------+
| 2014-06-13 05:00:00 | 2014-06-12 17:00:00                    |
+---------------------+----------------------------------------+
1 row in set (0.01 sec)


https://tech.pjin.jp/blog/2016/08/26/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f19/
mysql> select timestampdiff(year, p.birth, str_to_date('2014-06-13', '%Y-%m-%d')) as age, count(p.id) as count from players as p group by age;
+------+-------+
| age  | count |
+------+-------+
|   18 |     2 |
|   19 |     7 |
|   20 |    16 |
|   21 |    36 |
|   22 |    40 |
|   23 |    53 |
|   24 |    62 |
|   25 |    63 |
|   26 |    61 |
|   27 |    80 |
|   28 |    73 |
|   29 |    65 |
|   30 |    51 |
|   31 |    37 |
|   32 |    33 |
|   33 |    26 |
|   34 |    15 |
|   35 |     8 |
|   36 |     4 |
|   37 |     2 |
|   38 |     1 |
|   42 |     1 |
+------+-------+
22 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2016/08/26/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f20/
mysql> select timestampdiff(year, p.birth, str_to_date('2014-06-13', '%Y-%m-%d')) div 10 * 10 as age, count(p.id) as count from players as p group by age;
+------+-------+
| age  | count |
+------+-------+
|   10 |     9 |
|   20 |   549 |
|   30 |   177 |
|   40 |     1 |
+------+-------+
4 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/09/01/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f21/
mysql> select timestampdiff(year, p.birth, str_to_date('2014-06-13', '%Y-%m-%d')) div 5 * 5 as age, count(p.id) as count from players as p group by age;
+------+-------+
| age  | count |
+------+-------+
|   15 |     9 |
|   20 |   207 |
|   25 |   342 |
|   30 |   162 |
|   35 |    15 |
|   40 |     1 |
+------+-------+
6 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2016/09/01/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f22/
mysql> select timestampdiff(year, p.birth, str_to_date('2014-06-13', '%Y-%m-%d')) div 5 * 5 as age, p.position, count(p.id) as count, avg(height), avg(weight) from players as p group by age, p.position order by age asc, p.position asc;
+------+----------+-------+-------------+-------------+
| age  | position | count | avg(height) | avg(weight) |
+------+----------+-------+-------------+-------------+
|   15 | DF       |     2 |    185.0000 |     77.5000 |
|   15 | FW       |     3 |    179.0000 |     72.0000 |
|   15 | MF       |     4 |    175.0000 |     66.0000 |
|   20 | DF       |    61 |    183.9672 |     77.1639 |
|   20 | FW       |    51 |    179.0392 |     73.2353 |
|   20 | GK       |    14 |    187.6429 |     80.5000 |
|   20 | MF       |    81 |    178.9383 |     73.0741 |
|   25 | DF       |   113 |    183.3982 |     77.7080 |
|   25 | FW       |    63 |    181.1429 |     76.2381 |
|   25 | GK       |    45 |    188.6889 |     82.9111 |
|   25 | MF       |   121 |    179.4793 |     74.3306 |
|   30 | DF       |    57 |    181.1053 |     76.3509 |
|   30 | FW       |    32 |    180.9063 |     77.1875 |
|   30 | GK       |    31 |    186.0968 |     83.3548 |
|   30 | MF       |    42 |    178.1905 |     74.6667 |
|   35 | DF       |     3 |    189.0000 |     84.3333 |
|   35 | FW       |     3 |    184.3333 |     83.3333 |
|   35 | GK       |     5 |    186.8000 |     84.2000 |
|   35 | MF       |     4 |    178.7500 |     74.5000 |
|   40 | GK       |     1 |    191.0000 |     94.0000 |
+------+----------+-------+-------------+-------------+
20 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2016/09/11/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f23/
mysql> select p.name, p.height, p.weight from players as p order by p.height desc limit 5;
+-----------------------+--------+--------+
| name                  | height | weight |
+-----------------------+--------+--------+
| フォースター          |    201 |     99 |
| クルトワ              |    199 |     91 |
| メルテザッカー        |    198 |     90 |
| フェイジッチ          |    198 |     95 |
| バンビュイテン        |    197 |     95 |
+-----------------------+--------+--------+
5 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/09/11/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f24/
mysql> select p.name, p.height, p.weight from players as p order by p.height desc limit 15 offset 5;
+-----------------------+--------+--------+
| name                  | height | weight |
+-----------------------+--------+--------+
| ベゴビッチ            |    196 |     83 |
| ハート                |    196 |     89 |
| スマイラ              |    196 |     80 |
| コアテス              |    196 |     85 |
| カピノ                |    196 |     86 |
| ゴンザレス            |    196 |     93 |
| キム・シンウク        |    196 |     93 |
| ベルカレム            |    195 |     90 |
| ガブリエル            |    195 |     80 |
| エグウエクウェ        |    195 |     91 |
| アンドゥハル          |    194 |     88 |
| フェライニ            |    194 |     85 |
| スターリング          |    194 |     90 |
| ルイジコフ            |    194 |     92 |
| ウチェボ              |    194 |     86 |
+-----------------------+--------+--------+
15 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2016/10/29/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f28/
mysql> select * from players where birth <= date_add('2016-01-13', interval -40 year);
+-----+------------+-------------+----------+--------------------+-----------------------------------+------------+--------+--------+
| id  | country_id | uniform_num | position | name               | club                              | birth      | height | weight |
+-----+------------+-------------+----------+--------------------+-----------------------------------+------------+--------+--------+
| 185 |          9 |          22 | GK       | モンドラゴン       | デポルティボ・カリ                | 1971-06-21 |    191 |     94 |
| 188 |          9 |           3 | DF       | ジェペス           | アタランタ（イタリア）            | 1976-01-13 |    186 |     83 |
+-----+------------+-------------+----------+--------------------+-----------------------------------+------------+--------+--------+


https://tech.pjin.jp/blog/2017/04/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f51/
mysql> select (case player_id is null when 1 then '9999' else player_id end) as player_id, goal_time from goals order by id desc limit 10;
+-----------+-------------+
| player_id | goal_time   |
+-----------+-------------+
| 9999      | 後半47分    |
| 9999      | 前半11分    |
| 9999      | 前半31分    |
| 9999      | 前半3分     |
| 9999      | 後半3分     |
| 731       | 前半16分    |
| 730       | 前半46分    |
| 713       | 後半27分    |
| 710       | 後半23分    |
| 709       | 後半5分     |
+-----------+-------------+
10 rows in set (0.00 sec)

mysql> select (case when player_id is null then '9999' else player_id end) as player_id, goal_time from goals order by id desc limit 10;
+-----------+-------------+
| player_id | goal_time   |
+-----------+-------------+
| 9999      | 後半47分    |
| 9999      | 前半11分    |
| 9999      | 前半31分    |
| 9999      | 前半3分     |
| 9999      | 後半3分     |
| 731       | 前半16分    |
| 730       | 前半46分    |
| 713       | 後半27分    |
| 710       | 後半23分    |
| 709       | 後半5分     |
+-----------+-------------+


https://tech.pjin.jp/blog/2017/06/08/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f59/
mysql> select c.name, p.name, g.goal_time from goals as g join players as p on g.player_id = p.id join countries c on p.country_id = c.id limit 10;
+--------------+-----------------------------+-------------+
| name         | name                        | goal_time   |
+--------------+-----------------------------+-------------+
| ブラジル     | チアゴシウバ                | 前半7分     |
| ブラジル     | チアゴシウバ                | 前半7分     |
| ブラジル     | ダビドルイス                | 前半18分    |
| ブラジル     | フェルナンジーニョ          | 後半39分    |
| ブラジル     | オスカル                    | 後半46分    |
| ブラジル     | オスカル                    | 後半45分    |
| ブラジル     | フレジ                      | 後半4分     |
| ブラジル     | ネイマール                  | 前半29分    |
| ブラジル     | ネイマール                  | 後半26分    |
| ブラジル     | ネイマール                  | 前半17分    |
+--------------+-----------------------------+-------------+
10 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2017/07/01/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f60/
mysql> select g.goal_time, p.uniform_num, p.position, p.name from goals as g left outer join players as p on g.player_id = p.id;
| 延前15分    |           9 | FW       | ルカク                      |
| 後半43分    |          17 | FW       | オリジ                      |
| 後半29分    |          11 | FW       | ケルジャコフ                |
| 前半6分     |           9 | FW       | ココリン                    |
| 前半28分    |           5 | DF       | ハリシェ                    |
| 前半25分    |          10 | MF       | フェグリ                    |
| 後半17分    |          11 | MF       | ブラヒミ                    |
| 延後16分    |          18 | MF       | ジャブ                      |
| 前半38分    |          18 | MF       | ジャブ                      |
| 延後16分    |          18 | MF       | ジャブ                      |
| 後半15分    |          13 | FW       | スリマニ                    |
| 前半26分    |          13 | FW       | スリマニ                    |
| 後半5分     |           9 | MF       | ソン・フンミン              |
| 後半23分    |          11 | FW       | イ・グノ                    |
| 後半27分    |          13 | FW       | ク・ジャチョル              |
| 前半46分    |           9 | FW       | 岡崎                        |
| 前半16分    |           4 | FW       | 本田                        |
| 後半3分     |        NULL | NULL     | NULL                        |
| 前半3分     |        NULL | NULL     | NULL                        |
| 前半31分    |        NULL | NULL     | NULL                        |
| 前半11分    |        NULL | NULL     | NULL                        |
| 後半47分    |        NULL | NULL     | NULL                        |
+-------------+-------------+----------+-----------------------------+
188 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2017/07/01/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E5%95%8F61/
mysql> select g.goal_time, p.uniform_num, p.name from players as p right outer join goals as g on p.id = g.player_id;
| 前半38分    |          18 | ジャブ                      |
| 延後16分    |          18 | ジャブ                      |
| 後半15分    |          13 | スリマニ                    |
| 前半26分    |          13 | スリマニ                    |
| 後半5分     |           9 | ソン・フンミン              |
| 後半23分    |          11 | イ・グノ                    |
| 後半27分    |          13 | ク・ジャチョル              |
| 前半46分    |           9 | 岡崎                        |
| 前半16分    |           4 | 本田                        |
| 後半3分     |        NULL | NULL                        |
| 前半3分     |        NULL | NULL                        |
| 前半31分    |        NULL | NULL                        |
| 前半11分    |        NULL | NULL                        |
| 後半47分    |        NULL | NULL                        |
+-------------+-------------+-----------------------------+
188 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2017/07/10/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f62/
mysql> select c.name, g.goal_time, p.position, p.name from goals as g left outer join players as p on g.player_id = p.id left outer join countries as c on p.country_id = c.id;
| アルジェリア                         | 後半17分    | MF       | ブラヒミ                    |
| アルジェリア                         | 延後16分    | MF       | ジャブ                      |
| アルジェリア                         | 前半38分    | MF       | ジャブ                      |
| アルジェリア                         | 延後16分    | MF       | ジャブ                      |
| アルジェリア                         | 後半15分    | FW       | スリマニ                    |
| アルジェリア                         | 前半26分    | FW       | スリマニ                    |
| 韓国                                 | 後半5分     | MF       | ソン・フンミン              |
| 韓国                                 | 後半23分    | FW       | イ・グノ                    |
| 韓国                                 | 後半27分    | FW       | ク・ジャチョル              |
| 日本                                 | 前半46分    | FW       | 岡崎                        |
| 日本                                 | 前半16分    | FW       | 本田                        |
| NULL                                 | 後半3分     | NULL     | NULL                        |
| NULL                                 | 前半3分     | NULL     | NULL                        |
| NULL                                 | 前半31分    | NULL     | NULL                        |
| NULL                                 | 前半11分    | NULL     | NULL                        |
| NULL                                 | 後半47分    | NULL     | NULL                        |
+--------------------------------------+-------------+----------+-----------------------------+
188 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2017/07/10/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f63/
mysql> select p.kickoff, c.name, ec.name from pairings as p join countries as c on p.my_country_id = c.id join countries as ec on p.enemy_country_id = ec.id limit 10;
+---------------------+--------------------------+-----------------------+
| kickoff             | name                     | name                  |
+---------------------+--------------------------+-----------------------+
| 2014-06-13 05:00:00 | ブラジル                 | クロアチア            |
| 2014-06-14 01:00:00 | メキシコ                 | カメルーン            |
| 2014-06-14 04:00:00 | スペイン                 | オランダ              |
| 2014-06-14 07:00:00 | チリ                     | オーストラリア        |
| 2014-06-15 01:00:00 | コロンビア               | ギリシャ              |
| 2014-06-15 04:00:00 | ウルグアイ               | コスタリカ            |
| 2014-06-15 07:00:00 | イングランド             | イタリア              |
| 2014-06-15 10:00:00 | コートジボワール         | 日本                  |
| 2014-06-16 01:00:00 | スイス                   | エクアドル            |
| 2014-06-16 04:00:00 | フランス                 | ホンジュラス          |
+---------------------+--------------------------+-----------------------+
10 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2017/08/09/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E5%95%8F64/
mysql> select g.id, g.goal_time, (select p.name from players as p where g.player_id = p.id) as name from goals as g where g.player_id is not null limit 10;
+----+-------------+-----------------------------+
| id | goal_time   | name                        |
+----+-------------+-----------------------------+
|  1 | 前半7分     | チアゴシウバ                |
|  2 | 前半7分     | チアゴシウバ                |
|  3 | 前半18分    | ダビドルイス                |
|  4 | 後半39分    | フェルナンジーニョ          |
|  5 | 後半46分    | オスカル                    |
|  6 | 後半45分    | オスカル                    |
|  7 | 後半4分     | フレジ                      |
|  8 | 前半29分    | ネイマール                  |
|  9 | 後半26分    | ネイマール                  |
| 10 | 前半17分    | ネイマール                  |
+----+-------------+-----------------------------+
10 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2017/08/09/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E5%95%8F65/
mysql> select g.id, g.goal_time, p.name as name from goals as g inner join players as p on g.player_id = p.id where g.player_id is not null limit 10;
+----+-------------+-----------------------------+
| id | goal_time   | name                        |
+----+-------------+-----------------------------+
|  1 | 前半7分     | チアゴシウバ                |
|  2 | 前半7分     | チアゴシウバ                |
|  3 | 前半18分    | ダビドルイス                |
|  4 | 後半39分    | フェルナンジーニョ          |
|  5 | 後半46分    | オスカル                    |
|  6 | 後半45分    | オスカル                    |
|  7 | 後半4分     | フレジ                      |
|  8 | 前半29分    | ネイマール                  |
|  9 | 後半26分    | ネイマール                  |
| 10 | 前半17分    | ネイマール                  |
+----+-------------+-----------------------------+
10 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2017/08/26/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E5%95%8F66/
mysql> select p.position, p.height, p.name, p.club from (select position, max(height) as height from players group by position) as highest join players as p on highest.position = p.position and highest.height = p.height;
+----------+--------+-----------------------+-----------------------------------------------+
| position | height | name                  | club                                          |
+----------+--------+-----------------------+-----------------------------------------------+
| GK       |    201 | フォースター          | セルティック（スコットランド）                |
| MF       |    195 | ガブリエル            | ベヘレン（ベルギー）                          |
| DF       |    198 | メルテザッカー        | アーセナル（イングランド）                    |
| FW       |    196 | キム・シンウク        | 蔚山現代                                      |
+----------+--------+-----------------------+-----------------------------------------------+
4 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2017/08/26/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E5%95%8F67/
mysql> select p.position, max(p.height) as height, (select innerp.name from players as innerp where innerp.height = max(p.height) and innerp.position = p.position) as name from players as p group by position;
+----------+--------+-----------------------+
| position | height | name                  |
+----------+--------+-----------------------+
| DF       |    198 | メルテザッカー        |
| FW       |    196 | キム・シンウク        |
| GK       |    201 | フォースター          |
| MF       |    195 | ガブリエル            |
+----------+--------+-----------------------+
4 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2017/09/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f68/
mysql> select p.uniform_num, p.position, p.name, p.height from players as p where p.height < (select avg(height) from players);
+-------------+----------+--------------------------------------+--------+
| uniform_num | position | name                                 | height |
+-------------+----------+--------------------------------------+--------+
|          14 | DF       | マックスウェル                       |    176 |
|           2 | DF       | アウベス                             |    173 |
|           6 | DF       | マルセロ                             |    172 |
|           5 | MF       | フェルナンジーニョ                   |    175 |
|          18 | MF       | エルナネス                           |    181 |
|          16 | MF       | ラミレス                             |    180 |
|          19 | MF       | ビリアン                             |    174 |
|          11 | MF       | オスカル                             |    180 |
|           7 | FW       | フッキ                               |    180 |
|          10 | FW       | ネイマール                           |    175 |
|          20 | FW       | ベルナルジ                           |    163 |
|          12 | GK       | コロナ                               |    178 |


https://tech.pjin.jp/blog/2017/09/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f69/
mysql> select sub.group_name, sub.max, sub.min from (select c.group_name as group_name, max(ranking) as max, min(ranking) as min from countries as c group by c.group_name) as sub where (sub.max - sub.min) > 50;
+------------+------+------+
| group_name | max  | min  |
+------------+------+------+
| A          |   56 |    3 |
| B          |   62 |    1 |
+------------+------+------+
2 rows in set (0.00 sec)

mysql> select c.group_name, max(ranking), min(ranking) from countries as c group by c.group_name having max(ranking) - min(ranking) > 50;
+------------+--------------+--------------+
| group_name | max(ranking) | min(ranking) |
+------------+--------------+--------------+
| A          |           56 |            3 |
| B          |           62 |            1 |
+------------+--------------+--------------+
2 rows in set (0.00 sec)


https://tech.pjin.jp/blog/2017/09/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f70/
mysql> select 1980 as year, count(id) from players where birth like '1980%' union select 1981 as year, count(id) from players where birth like '1981%';
+------+-----------+
| year | count(id) |
+------+-----------+
| 1980 |        19 |
| 1981 |        31 |
+------+-----------+
2 rows in set (0.01 sec)


https://tech.pjin.jp/blog/2017/09/30/sql%e7%b7%b4%e7%bf%92%e5%95%8f%e9%a1%8c-%e5%95%8f71/
mysql> select p.id, p.position, p.name, p.height, p.weight from players as p where height > 195 union all select p.id, p.position, p.name, p.height, p.weight from players as p where weight > 95 order by id asc;
+-----+----------+-----------------------+--------+--------+
| id  | position | name                  | height | weight |
+-----+----------+-----------------------+--------+--------+
| 210 | GK       | カピノ                |    196 |     86 |
| 308 | DF       | コアテス              |    196 |     85 |
| 324 | GK       | ハート                |    196 |     89 |
| 325 | GK       | フォースター          |    201 |     99 |
| 325 | GK       | フォースター          |    201 |     99 |
| 462 | GK       | フェイジッチ          |    198 |     95 |
| 463 | GK       | ベゴビッチ            |    196 |     83 |
| 534 | DF       | メルテザッカー        |    198 |     90 |
| 583 | DF       | ゴンザレス            |    196 |     93 |
| 607 | DF       | スマイラ              |    196 |     80 |
| 624 | GK       | クルトワ              |    199 |     91 |
| 625 | DF       | バンビュイテン        |    197 |     95 |
| 642 | FW       | ルカク                |    190 |    100 |
| 712 | FW       | キム・シンウク        |    196 |     93 |
+-----+----------+-----------------------+--------+--------+
14 rows in set (0.00 sec)
```

