# Комментарии к коду 

### Импорт библиотек
```python
import tkinter as tk
from tkinter import ttk
import sqlite3
``` 

### Класс Main
```python
class Main(tk.Frame):
    def init(self, root):
        super().init(root)
        self.init_main()
        self.db = db
        self.view_records()
```
- Начало объявления класса `Main`, который наследуется от класса `tk.Frame`
- Метод `init` используется для инициализации основного окна приложения, задания главного меню, создания базы данных и отображения записей в таблице.

```python
    def init_main(self):
        toolbar = tk.Frame(bg="#d7d8e0", bd=2)
        toolbar.pack(side=tk.TOP, fill=tk.X)
``` 
- Метод `init_main` создает панель инструментов, задает ее внешний вид и расположение.

```python
        self.add_img = tk.PhotoImage(file="./img/add.png")
        btn_open_dialog = tk.Button(
            toolbar, bg="#d7d8e0", bd=0, image=self.add_img, command=self.open_dialog
        )
        btn_open_dialog.pack(side=tk.LEFT)
``` 
- Создание кнопки добавления записи с заданным изображением и командой для открытия диалогового окна.

```python
        self.tree = ttk.Treeview(
            self, columns=("ID", "name", "tel", "email"), height=45, show="headings"
        )

        self.tree.column("ID", width=30, anchor=tk.CENTER)
        self.tree.column("name", width=300, anchor=tk.CENTER)
        self.tree.column("tel", width=150, anchor=tk.CENTER)
        self.tree.column("email", width=150, anchor=tk.CENTER)

        self.tree.heading("ID", text="ID")
        self.tree.heading("name", text="ФИО")
        self.tree.heading("tel", text="Телефон")
        self.tree.heading("email", text="E-mail")

        self.tree.pack(side=tk.LEFT)
``` 
- Создание таблицы (располагается слева в основном окне), указание заголовков столбцов и их ширины.

```python
        self.update_img = tk.PhotoImage(file="./img/update.png")
        btn_edit_dialog = tk.Button(
            toolbar,
            bg="#d7d8e0",
            bd=0,
            image=self.update_img,
            command=self.open_update_dialog,
        )
        btn_edit_dialog.pack(side=tk.LEFT)
``` 
- Создание кнопки для открытия диалогового окна редактирования записей.

```python
        self.delete_img = tk.PhotoImage(file="./img/delete.png")
        btn_delete = tk.Button(
            toolbar,
            bg="#d7d8e0",
            bd=0,
            image=self.delete_img,
            command=self.delete_records,
        )
        btn_delete.pack(side=tk.LEFT)
``` 
- Создание кнопки для удаления выбранных записей.

```python
        self.search_img = tk.PhotoImage(file="./img/search.png")
        btn_search = tk.Button(
            toolbar,
            bg="#d7d8e0",
            bd=0,
            image=self.search_img,
            command=self.open_search_dialog,
        )
        btn_search.pack(side=tk.LEFT)
``` 
- Создание кнопки для открытия диалогового окна поиска.

```python
        self.refresh_img = tk.PhotoImage(file="./img/refresh.png")
        btn_refresh = tk.Button(
            toolbar,
            bg="#d7d8e0",
            bd=0,
            image=self.refresh_img,
            command=self.open_search_dialog,
        )
        btn_refresh.pack(side=tk.LEFT)
``` 
- Создание кнопки для обновления записей.

```python
    def open_dialog(self):
        Child()
``` 
- Метод `open_dialog` создает экземпляр класса `Child`, что открывает диалоговое окно для добавления записи.

```python
    def records(self, name, tel, email):
        self.db.insert_data(name, tel, email)
        self.view_records()
``` 
- Метод `records` добавляет новую запись в базу данных и обновляет таблицу с записями.

```python    
    def view_records(self):
        self.db.cursor.execute("SELECT * FROM db")
        [self.tree.delete(i) for i in self.tree.get_children()]
        [self.tree.insert("", "end", values=row) for row in self.db.cursor.fetchall()]
``` 
- Метод `view_records` выбирает все записи из базы данных, очищает таблицу и добавляет записи из базы данных в таблицу.

```python
    def open_update_dialog(self):
        Update()
``` 
- М
