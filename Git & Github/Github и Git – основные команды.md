## Как закомитить ваш код в репозиторий.  

#### На сайте

1) Создайте новый репозиторий на https://github.com 

![[Github_new_rep.png]]


2) Дайте название своему проекту и описание. Другие настройки можно не трогать
3) Используйте ссылку на репозиторий далее в одной из команд 

#### В терминале 

В директории вашего проекта вводите следующие команды последовательно

```sh
git init
```

Check the status of current project 
```sh
git status
```

Add, delete and update your files to the Git repository:
```sh
git add .
```

This adds all files in your current directory to the Git staging area. Or deletes files not exisiting anymore

Commit your changes:

```sh
git commit -m "Initial commit"
```

Replace "Initial commit" with a meaningful commit message describing your changes.

Link your local repository to the GitHub repository:

```sh
git remote add origin https://github.com/yourusername/yourprojectname.git
```

Replace "yourusername" with your GitHub username and "yourprojectname" with your repository name.

Push your changes to GitHub:

```sh
git push -u origin main
```


#git 