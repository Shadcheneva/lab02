
# Объявление Необходимых переменных
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>

# присвоение edit вызов удобного текстового редактора
$ alias edit=<nano|vi|vim|subl>

# переход в рабочую директорию
$ cd ${GITHUB_USERNAME}/workspace

# исполнение кода из файла activate
$ source scripts/activate

# создание директории
$ mkdir ~/.config

# запись текста до EOF в файл hub
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF

# установка параметров протокола гит
$ git config --global hub.protocol https

# создание новой директории lab02 и переход в нее
$ mkdir projects/lab02 && cd projects/lab02

# Создание гит-репозитория из этого каталога
$ git init

# Установка необходимых параметров гит(имя пользователя, е-маil)
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
#  check your git global settings
$ git config -e --global


# Добавление удалённого гит-репозиторий под именем-сокращением, к которому будет проще обращаться
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git

# Добавление в локальный сервер последнюю версию кода
$ git pull origin master

# создание нового файла
$ touch README.md

# Текущее состояние репозитория
$ git status

# Добавление файла в репозиторий
$ git add README.md

# сделать коммит с подписью "added README.md"
$ git commit -m "added README.md"

# слияние локального репозитория с гитхаб репозиторием
$ git push origin master


Добавить на сервисе GitHub в репозитории lab02 файл .gitignore со следующем содержимом:

*build*/
*install*/
*.swp
.idea/




# Добавление в локальный сервер последнюю версию кода
$ git pull origin master

# история изменений
$ git log

# Создание директорий
$ mkdir sources
$ mkdir include
$ mkdir examples

# создание и запись в файл print.cpp до EOF
$ cat > sources/print.cpp <<EOF
# include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF

# создание и запись в файл print.hpp до EOF
$ cat > include/print.hpp <<EOF
# include <fstream>
# include <iostream>
# include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF

# создание и запись в файл example1.cpp до EOF
$ cat > examples/example1.cpp <<EOF
# include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF

# создание и запись в файл example2.cpp до EOF
$ cat > examples/example2.cpp <<EOF
# include <print.hpp>

# include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF

# Редактирования файла
$ edit README.md

# текущее состояние репозитория
$ git status

# 
$ git add .

# Коммит с подписью " added sources"
$ git commit -m" added sources"

# слияние локального репозитория с гитхаб репозиторием
$ git push origin master
# Homework
# Part I
1.Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com). 
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02H.git
Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге. 
$ git pull origin master 
$ touch README.md 
$ git add README.md 
$ git commit -m"first commit" 
$ git push origin master
2.Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). 
3.Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;. 
$ mkdir sources 
$ mkdir examples 
$ cat > sources/hello_world.cpp <<EOF #include <hello_world.hpp> using namespace std
int main() { cout << "hello world" << endl; } EOF 
4. Добавьте этот файл в локальную копию репозитория. 
$ git add sources/hello_world.cpp 
5. Закоммитьте изменения с осмысленным сообщением. 
$ git commit -m"create hello_world.cpp" 
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя. 
$ edit sources/hello_world.cpp #include <hello_world.hpp> #include using namespace std

int main() { string name; cout << "enter your name" << endl; cin >> name; cout << endl << "hello world" << endl; } 
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно git add? Ответ: После изменений он сохранится автоматически 
8. Запуште изменения в удалёный репозиторий. 
$ git push origin master 
9. Проверьте, что история коммитов доступна в удалёный репозитории.

# Part II
Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

В локальной копии репозитория создайте локальную ветку patch1. 
$ git checkout -b patch1
Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std;. 
$ edit sources/hello_world.cpp <<EOF #include <hello_world.hpp> #include
int main() { std::string name; std::cout << "enter your name" << std::endl; std::cin >> name; std::cout << std::endl << "hello world" << std::endl; } EOF 
3. commit, push локальную ветку в удалённый репозиторий. 
$ git commit -m"change hello_world.cpp" 
$ git push origin patch1 
4. Проверьте, что ветка patch1 доступна в удалёный репозитории. 
5. Создайте pull-request patch1 -> master. 
6. В локальной копии в ветке patch1 добавьте в исходный код комментарии. 
$ edit sources/hello_world.cpp <<EOF #include <hello_world.hpp> #include

int main() { std::string name; // объявлена переменная типа string std::cout << "enter your name" << std::endl; // вывод строки "enter your name" std::cin >> name; // ввод строки в переменную name std::cout << std::endl << "hello world" << std::endl; // вывод строки "hello world" } EOF 
7. commit, push. 
$ git commit -m"add comments" 
$ git push origin patch1 
8. Проверьте, что новые изменения есть в созданном на шаге 5 pull-request 
9. В удалённый репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории. 
$ git checkout master 
$ git merge patch1 
10. Локально выполните pull. 
$ git pull origin master 
11. С помощью команды git log просмотрите историю в локальной версии ветки master. 
12. Удалите локальную ветку patch1.

# Part III
Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

Создайте новую локальную ветку patch2.
Измените code style с помощью утилиты clang-format. Например, используя опцию -style=Mozilla. 
$ sudo npm install -g clang-format 
$ clang-format -i -style=Mozilla sources/hello_world.cpp
commit, push, создайте pull-request patch2 -> master. 
$ git checkout -b patch2 
$ git commit -m"Mozilla style" 
$ git push origin patch2
В ветке master в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
Убедитесь, что в pull-request появились конфликты.
Для этого локально выполните pull + rebase (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты. 
$ git rebase master 
$ git rebase --continue
Сделайте force push в ветку patch2 
$ git push origin feature --force
Убедитель, что в pull-request пропали конфликты.
Вмержите pull-request patch2 -> master.
