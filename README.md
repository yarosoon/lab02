## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```console
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
```

```console
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```console
$ mkdir ~/.config
mkdir: cannot create directory ‘/home/ubuntu/.config’: File exists
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```console
$ mkdir projects/lab02 && cd projects/lab02
$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /home/ubuntu/yarosoon/workspace/projects/lab02/.git/
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 1.18 KiB | 1.18 MiB/s, done.
From https://github.com/yarosoon/lab02
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
$ touch README.md
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
  README.md

nothing added to commit but untracked files present (use "git add" to track)
$ git add README.md
$ git commit -m"added README.md"
[master c2dc499] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
$ git push origin master
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 278 bytes | 278.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/yarosoon/lab02/pull/new/master
remote: 
To https://github.com/yarosoon/lab02.git
 * [new branch]      master -> master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```console
$ git pull origin master
From https://github.com/yarosoon/lab02
 * branch            master     -> FETCH_HEAD
Already up to date.
$ git log
commit c2dc4991eeb429cc992c9f70efa8ebd0d19d0f55 (HEAD -> master, origin/master)
Author: yarosoon <p.nuikin@gmail.com>
Date:   Mon Mar 6 10:16:27 2023 +0300

    added README.md

commit 8e99ed6921511ae94bb6ae8d29a79940a75137d0 (origin/main)
Author: yarosoon <112762136+yarosoon@users.noreply.github.com>
Date:   Mon Mar 6 09:50:02 2023 +0300

    Initial commit
```

```console
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```console
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```console
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```console
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```console
$ edit README.md
```

```console
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    examples/
    include/
    sources/

no changes added to commit (use "git add" and/or "git commit -a")
$ git add .
$ git commit -m"added sources"
[master 9df4bee] added sources
 5 files changed, 33 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp
$ git push origin master
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 8 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (10/10), 1006 bytes | 1006.00 KiB/s, done.
Total 10 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/yarosoon/lab02.git
   c2dc499..9df4bee  master -> master
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.

```console
$ cd yarosoon/workspace/
$ source scripts/activate 
$ mkdir ~/.config
mkdir: cannot create directory ‘/home/ubuntu/.config’: File exists
$ mkdir projects/lab02_homework && cd projects/lab02_homework
$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /home/ubuntu/yarosoon/workspace/projects/lab02_homework/.git/
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
$ git config -e --global 
$ git remote add origin https://github.com/yarosoon/lab02_homework
$ git remote add origin https://github.com/yarosoon/lab02_homework.git
error: remote origin already exists.
$ git pull origin main
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 1.17 KiB | 1.17 MiB/s, done.
From https://github.com/yarosoon/lab02_homework
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
 $ touch README.md
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    README.md

nothing added to commit but untracked files present (use "git add" to track)
$ git add README.md
$ git commit -m"added README.md"
[master 5d83e0b] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
$ git push origin master 
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 279 bytes | 279.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/yarosoon/lab02_homework/pull/new/master
remote: 
To https://github.com/yarosoon/lab02_homework
 * [new branch]      master -> master
```

3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.

```console
$ mkdir sources
$ cat > sources/hello_world.cpp <<EOF
> #include <iostream>
> 
>using namespace std;
>
> int main()
> {
>   std::cout << "Hello, world!";
>   return 0;
> }
> EOF
```

4. Добавьте этот файл в локальную копию репозитория.

```console
$ git add sources/hello_world.cpp
```

5. Закоммитьте изменения с *осмысленным* сообщением.

```console
$ git commit -m"added hello_world.cpp"
```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.

```console
$ edit sources/hello_world.cpp
```

7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?

```console
$ git commit -m"fixed hello_world.cpp"
[master e0cbb84] fixed hello_world.cpp
 1 file changed, 4 insertions(+), 3 deletions(-)
```

8. Запуште изменения в удалёный репозиторий.

```console
$ git push origin master
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 438 bytes | 438.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/yarosoon/lab02_homework
   f794285..e0cbb84  master -> master
```

9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.

```console
$ git checkout -b patch1
Switched to a new branch 'patch1'
```

2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.

```console
$ edit sources/hello_world.cpp
```

3. **commit**, **push** локальную ветку в удалённый репозиторий.

```console
$ git commit -m"fixed hello_world.cpp"
On branch patch1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   sources/hello_world.cpp

no changes added to commit (use "git add" and/or "git commit -a")
$ git add sources/hello_world.cpp 
$ git commit -m"fixed hello_world.cpp"
[patch1 d092a5e] fixed hello_world.cpp
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git push origin patch1
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 337 bytes | 337.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/yarosoon/lab02_homework/pull/new/patch1
remote: 
To https://github.com/yarosoon/lab02_homework
 * [new branch]      patch1 -> patch1
```

4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.

```console
$ edit sources/hello_world.cpp
```

7. **commit**, **push**.

```console
$ git add sources/hello_world.cpp 
$ git commit -m"added comments to hello_world.cpp"
[patch1 9c4552f] added comments to hello_world.cpp
 1 file changed, 2 insertions(+)
$ git push origin patch1
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 380 bytes | 380.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/yarosoon/lab02_homework
   d092a5e..9c4552f  patch1 -> patch1
```

8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.

```console
$ git pull origin main
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), 614 bytes | 614.00 KiB/s, done.
From https://github.com/yarosoon/lab02_homework
 * branch            main       -> FETCH_HEAD
   ed43b5c..e074b74  main       -> origin/main
Updating 9c4552f..e074b74
Fast-forward
```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.

```console
$ git log
commit e074b7464ee4c1f520d807ee849de1f3c3f638eb (HEAD -> patch1, origin/main)
Merge: ed43b5c 9c4552f
Author: yarosoon <112762136+yarosoon@users.noreply.github.com>
Date:   Mon Mar 13 09:23:00 2023 +0300

    Merge pull request #1 from yarosoon/patch1
    
    Patch1

commit 9c4552fa4a333fbc217454029ce15cf15743548c (origin/patch1)
Author: yarosoon <p.nuikin@gmail.com>
Date:   Mon Mar 13 09:22:03 2023 +0300

    added comments to hello_world.cpp

commit d092a5e455c6b03b819008aa99261e1cc28cc03e
Author: yarosoon <p.nuikin@gmail.com>
Date:   Mon Mar 13 09:18:56 2023 +0300

    fixed hello_world.cpp

commit e0cbb840308bc0339406881c19a63430a9580568 (origin/master, master)
Author: yarosoon <p.nuikin@gmail.com>
Date:   Mon Mar 13 09:08:45 2023 +0300
```
12. Удалите локальную ветку `patch1`.

```console
$ git branch --delete patch1 
error: Cannot delete branch 'patch1' checked out at '/home/ubuntu/yarosoon/workspace/projects/lab02_homework'
$ git checkout master 
Switched to branch 'master'
$ git branch --delete patch1 
error: The branch 'patch1' is not fully merged.
If you are sure you want to delete it, run 'git branch -D patch1'.
$ git branch -D patch1 
Deleted branch patch1 (was e074b74).
```

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.

```console
$ git checkout -b patch2
Switched to a new branch 'patch2'
```

2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.

```console
$ clang-format -i --style=Mozilla sources/hello_world.cpp
```

3. **commit**, **push**, создайте pull-request `patch2 -> master`.

```console
$ git add sources/hello_world.cpp 
$ git commit -m"changed code-style"
[patch2 15e9b20] changed code-style
 1 file changed, 2 insertions(+), 1 deletion(-)
$ git push origin patch2 
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 338 bytes | 338.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/yarosoon/lab02_homework/pull/new/patch2
remote: 
To https://github.com/yarosoon/lab02_homework
 * [new branch]      patch2 -> patch2
```

4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликты*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.

```console
$ git pull --rebase origin 
error: Pulling is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.
$ git status
interactive rebase in progress; onto efe4b02
Last command done (1 command done):
   pick 15e9b20 changed code-style
No commands remaining.
You are currently rebasing branch 'patch2' on 'efe4b02'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
    both modified:   sources/hello_world.cpp

no changes added to commit (use "git add" and/or "git commit -a")
$ git add sources/hello_world.cpp 
$ git rebase --continue 
[detached HEAD fa5db1c] changed code-style
 1 file changed, 5 insertions(+)
Successfully rebased and updated refs/heads/patch2.
```

7. Сделайте *force push* в ветку `patch2`

```console
$ git push origin patch2 --force
Username for 'https://github.com': yarosoon
Password for 'https://yarosoon@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 400 bytes | 400.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/yarosoon/lab02_homework
```

8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
