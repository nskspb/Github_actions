# Github_actions

GitHub Actions — это сервис автоматизации тестирования и доставки кода на продакшен. Пайплайн доставки кода, в терминологии GitHub — workflow, описывается в yml-файле и размещается непосредственно в рабочем репозитории в директории .GitHub/workflows/[workflowname].yml.

На уровне workflow определяется название workflow и триггер — условие, при котором будет срабатывать workflow. В коде эта инструкция выглядит так:

name: test_workflow #Название workflow
on: push #Триггер исполнения workflow. 
В данном случае workflow будет вызван автоматически при загрузке или обновления кода в репозитории.
Workflow состоит из jobs (джобы) — это логический уровень задачи. 
На уровне jobs определяется ОС, в среде которой будет выполняться задача и определяются шаги, которые содержат команды — инструкция run или экшены — инструкция uses. 
В коде это может выглядеть так:

name: print hello and checkout repo workflowc <br />
on: push <br />
<br />
jobs: <br />
<br />
  print_hello:<br />
    runs-on: ubuntu-latest<br />
    steps:<br />
      - name: Print hello<br />
        run: echo "Hello world!"<br />
<br />
  checkout_repo:<br />
    runs-on: ubuntu-latest<br />
    steps:<br />
      - name: checkout<br />
        uses: actions/checkout@v3<br />
По умолчанию джобы и workflow выполняются параллельно на разных VM GitHub. Этим поведением можно управлять и выстраивать цепочки. Для последовательного и связанного выполнения джобов, 
в зависимых джобах используется инструкция needs: [waiting job]. 
Вот пример связанных джобов:<br />
<br />
jobs:<br />
<br />
  print_hello:<br />
    runs-on: ubuntu-latest<br />
    steps:<br />
      - name: Print hello<br />
        run: echo "Hello world!"<br />
<br />
  checkout_repo:<br />
    needs: print_hellow<br />
    runs-on: ubuntu-latest<br />
    steps:<br />
      - name: checkout<br />
        uses: actions/checkout@v3 <br />