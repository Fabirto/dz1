$ sudo apt update && sudo apt install wget
устанавливает wget
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
скачивает файл

$ mkdir -p ~/boost_1_69_0
$ tar -xzf boost_1_69_0.tar.gz -C ~/boost_1_69_0 --strip-components=1
-xzf — распаковывает (x) gzip-архив (z) в файл (f).
-C ~/boost_1_69_0 — указывает папку для распаковки.
--strip-components=1 — убирает верхнюю папку из архива (чтобы файлы были прямо в ~/boost_1_69_0, а не в ~/boost_1_69_0/boost_1_69_0/).
    
find ~/boost_1_69_0 -maxdepth 1 -type f | wc -l (вывел 12)

ищет в директории, не заходит в поддиректорию, ищет только файлы

find ~/boost_1_69_0 -type f | wc -l (вывел 61191)

тоже ищет в директории, но заходит в поддиректории

find ~/boost_1_69_0 -type f \( -name "*.h" -o -name "*.hpp" -o -name "*.hxx" \) | wc -l
подсчет заголовочных файлов (15208)

find ~/boost_1_69_0 -type f -name "*.cpp" | wc -l
подсчет файлов .cpp (13774)

find ~/boost_1_69_0 -type f -not \( -name "*.h" -o -name "*.hpp" -o -name "*.hxx" -o -name "*.cpp" \) | wc -l
подсчет остальных файлов (32209)

find ~/boost_1_69_0 -type f -name "any.hpp" -print
находит файл и показывает путь к нему
/home/vboxuser/boost_1_69_0/boost/proto/detail/any.hpp
/home/vboxuser/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
/home/vboxuser/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
/home/vboxuser/boost_1_69_0/boost/hana/fwd/any.hpp
/home/vboxuser/boost_1_69_0/boost/hana/any.hpp
/home/vboxuser/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
/home/vboxuser/boost_1_69_0/boost/fusion/algorithm/query/any.hpp
/home/vboxuser/boost_1_69_0/boost/fusion/include/any.hpp
/home/vboxuser/boost_1_69_0/boost/any.hpp
/home/vboxuser/boost_1_69_0/boost/type_erasure/any.hpp


grep -rl "boost::asio" ~/boost_1_69_0
выводит в консоль все файлы, где упоминается последовательность boost::asio.



sudo apt update
sudo apt install build-essential g++ python3-dev autotools-dev libicu-dev libbz2-dev
cd ~/boost_1_69_0
./bootstrap.sh 
./b2
компилирует



mkdir -p ~/boost-libs
find ~/boost_1_69_0/stage/lib -name "*.a" -exec cp {} ~/boost-libs \;
переносит файлы в boost-libs


du -ah ~/boost-libs | sort -rh
показывает размер всех файлов, сортирует по разиеоу


du -ah ~/boost-libs | sort -rh | head -n 10
выводит 10 самых тяжелых 
29M	/home/vboxuser/boost-libs
4.5M	/home/vboxuser/boost-libs/libboost_wave.a
3.1M	/home/vboxuser/boost-libs/libboost_regex.a
2.8M	/home/vboxuser/boost-libs/libboost_math_tr1l.a
2.8M	/home/vboxuser/boost-libs/libboost_math_tr1.a
2.7M	/home/vboxuser/boost-libs/libboost_math_tr1f.a
2.3M	/home/vboxuser/boost-libs/libboost_unit_test_framework.a
2.3M	/home/vboxuser/boost-libs/libboost_test_exec_monitor.a
1.6M	/home/vboxuser/boost-libs/libboost_program_options.a
1.2M	/home/vboxuser/boost-libs/libboost_serialization.a


