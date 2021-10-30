# [SQL練習問題 – 一覧まとめ](https://tech.pjin.jp/blog/2016/12/05/sql%E7%B7%B4%E7%BF%92%E5%95%8F%E9%A1%8C-%E4%B8%80%E8%A6%A7%E3%81%BE%E3%81%A8%E3%82%81/)

```
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

