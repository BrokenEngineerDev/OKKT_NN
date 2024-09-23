## [Антоненко Дмитро Юрійович](https://github.com/BrokenEngineerDev)


# МІНІСТЕРСТВО ОСВІТИ І НАУКИ УКРАЇНИ 
## ОДЕСЬКИЙ ФАХОВИЙ КОЛЕДЖ КОМП’ЮТЕРНИХ ТЕХНОЛОГІЙ

#### Практична частина дисципліни "Основи штучних нейронних мереж"

#### Лабораторна робота №2

#### Стандартні бібліотеки для роботи з даними та їх візуалізацією


1. Створюємо `CodeCell` та імпортуємо в ньому бібліотку `pandas` одразу використовуючи alias `pd` для скорочення виклику бібліотекі


    ```python
    import pandas as pd
    ```

    Якщо бібліотекі немає у вашому Python Kernel до потрібно її встановити командою

    ```console
    pip install pandas
    ```
2. Використовуючи метод `pd.read_csv()`, імпортуємо данні з файлу [iris.csv](iris.csv) 

    - Метод приймає у якості параметра шлях до вашого файлу від місця виконання, так як виконуванний файл [lab02.ipynb](lab02.ipynb) знаходиться у тому ж каталозі, то можему вказати просто ім'я файлу

        Якби файл знаходився у каталозі вище, наприклад `OKKT_NN` то тоді шлях вказувався б з використанням `..` і виглядав би ось так `../iris.csv`

        У випадку з підкаталагом, то вказували б відносний шлях від місця виконання і виглядав би ось так `folder/iris.csv`
   -  Метод віддає данні у форматі `DataFrame`, який має табличну структуру схожу на Excel
      -  `row` - це конкретні записи 
      -  `column` - це характеристики
    ```python
    df = pd.read_csv('iris.csv')
    ```

3. Використовучи метод `df.head()` виводимо зображення 5 перших записів з набору данних
    ```python
    df.head()
    ```
4. Використовучи метод `df.info()` виводимо загальну інформацію про датасет
   ```python
   df.info()
   ```
5. Групування даних за видом квітки і обчислення середнього 
    ```python
    df.groupby('Species').mean()
    ```
6. Імпорт бібліотеки Matplotlib та одразу використовуємо alias `plt`
    - Вона потрібна для візулізації та побудови графіків
    ```python
    import matplotlib.pyplot as plt
    ```
    Якщо бібліотекі немає у вашому Python Kernel до потрібно її встановити командою
    ```console
    pin install matplotlib
    ```
7. Побудова графіку по параметру `SepalLengthCm`
    ```
    plt.plot(df['SepalLengthCm'])
    ```
8. Гістограмма по параметрам датасету
    ```python
    df.hist(bins=50, figsize=(20, 20))
    plt.show()
    ```
9. Парні діаграми (pairplot) - дозволяє побачити взаємозвязок між усіма парами атрибутів
    - Для її побудування потрібно імпортувати бібліотеку `seaborn`
  
    ```python
    import seaborn as sns
    ```

    - Та викликати метод `pairplot` для побудови графіка
    ```python
    sns.pairplot(df, hue='Species')
    ```

    Якщо бібліотекі немає у вашому Python Kernel до потрібно її встановити командою

    ```console
    pip install seaborn
    ```
10. BoxPlot - показує розподіл даних для числового значення атрибуту
    ```python
    sns.boxplot(x='Species', y='PetalLengthCm', data=df)
    plt.show()
    ```
11. Дозволяє візуалізувати взаємозв'язок між двома числовими змінними, забарвлюючи точки в різні кольори залежно від виду ірису
    ```python
    sns.scatterplot(x='PetalLengthCm', y='PetalWidthCm', hue='Species', data=df)
    
    plt.show()
    ```

12. Комплексна візуалізація
    
    ```python
    
        fig, axes = plt.subplots(2, 2, figsize=(12, 8))

        sns.histplot(data=df, x='PetalLengthCm', hue='Species', ax=axes[0, 0])
        sns.histplot(data=df, x='PetalWidthCm', hue='Species', ax=axes[0, 1])

        sns.boxplot(x='Species', y='SepalLengthCm', data=df, ax=axes[1, 0])
        sns.boxplot(x='Species', y='SepalWidthCm', data=df, ax=axes[1, 1])

        plt.tight_layout()
        plt.show()
    ```