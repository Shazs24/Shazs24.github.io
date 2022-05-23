# Shazs24.github.io
Мой сайт

  1. import random
  2. HANGMANPICS = ['''
  3.
  4.    +---+
  5.    |   |
  6.        |
  7.        |
  8.        |
  9.        |
 10. =========''','''
 11.
 12.    +---+
 13.    |   |
 14.    O   |
 15.        |
 16.        |
 17.        |
 18. =========''','''
 19.
 20.    +---+
 21.    |   |
 22.    O   |
 23.    |   |
 24.        |
 25.        |
 26. =========''','''
 27.
 28.    +---+
 29.    |   |
 30     O   |
 31.   /|   |
 32.        |
 33.        |
 34. =========''','''
 35.
 36.    +---+
 37.    |   |
 38.    O   |
 39.   /|\  |
 40.        |
 41.        |
 42. =========''','''
 43.
 44.    +---+
 45.    |   |
 46.    O   |
 47.   /|\  |
 48.   /    |
 49.        |
 50. =========''','''
 51.
 52.    +---+
 53.    |   |
 54.    O   |
 55.   /|\  |
 56.   / \  |
 57.        |
 58. =========''']
 59.
 60. words = 'муравей бабуин барсук медведь бобр верблюд 
кошка моллюск кобра пума койот ворона олень собака осел 
утка орел хорек лиса лягушка коза гусь ястреб ящерица лама 
моль обезьяна лось мышь мул тритон выдра сова панда попугай 
голубь питон кролик баран крыса носорог лосось акула змея 
паук аист лебедь тигр жаба форель индейка черепаха ласка 
кит волк вомбат зебра'.split()
 61.
 62. def getRandomWord(wordList):
 63.     #Эта функция возвращает случайное слово, которое выбирает из заранее 
созданного списка
 64.     wordIndex = random.randint(0, len(wordList) - 1)
 65.     return wordList[wordIndex]
 66.
 67. def displayBoard(HANGMANPICS, missedletters, correctLetters,secretWord):
 68.     print(HANGMANPICS[len(missedLetters)])
 69.     print()
 70. 
 71.     print('Неправильные буквы:', end=' ')
 72.     for letter in missedLetters:
 73.         print(letter, end=' ')
 74.     print()
 75.
 76.     blanks = '*'*len(secretWord)
 77.     #Заменяем звездочки на правильно угаданные буквы
 78.     for i in range(len(secretWord)):
 79.         if secretWord[i] in correctLetters:
 80.             blanks = blanks[:i] + secretWord[i] + blanks[i+1:]
 81.     #Показываем загаданное слово с пробелами между букв
 82.     for letter in blanks: 
 83.         print(letter, end=' ')
 84.     print()
 85.
 86. def getGuess(alreadyGuessed):
 87.     #Возвращает букву, которую ввел игрок. Эта функция проверяет, что введена
 буква, а не какой-то другой символ
 88.     while True:
 89.     print('Введите букву')
 90.     guess = input()
 91.     guess = guess.lower()
 92.     if len(guess) != 1:
 93          print('Ваша буква:')
 94.     elif guess in alreadyGuessed:
 95.         print ('Вы уже пробовали эту букву. Выберите другую')
 96.     elif guess not in 'ёйцукенгшщзхъфывапролджэячсмитьбю':
 97.         print('Пожалуйста, введите букву кириллицы')
 98.     else:
 99.         return guess
100.
101. def playAgain():
102.     #Эта функция возвращает True если игрок решит сыграть еще раз. 
В противном случае возвращается False
103.     print('Хотите попробовать еще раз? ("Да" или "Нет")')
104.     return input().lower().startswith('д')
105.
106. print('В И С Е Л И Ц А')
107. missedLetters = ''
108. correctLetters = ''
109. secretWord = getRandomWord(words)
110. gameIsDone = False
111.
112. while True:
113.     displayBoard(HANGMANPICS, missedLetters, correctLetters, secretWord)
114.
115.     #Вычисляем количество букв, которые ввел игрок
116.
117.     guess = getGuess(missedLetters+correctLetters)
118.
119.     if guess in secretWord:
120.         correctLetters = correctLetters + guess
121.
122.         #Проверка условия победы игрока
123.         foundAllLetters = True
124.         for i in range(len(secretWord)):
125.             if secretWord[i] not in correctLetters:
126.                 foundAllLetters = False
127.                 break
128.         if foundAllLetters:
129.             print('Превосходно! Было загадано слово "'+secretWord+'"
! Вы победили!')
130.
131.             gameIsDone = True
132.     else:
133.         missedLetters = missedLetters+guess
134.
135.         #Проверка условия проигрыша игрока
136.         if len(missedLetters) == len(HANGMANPICS) - 1:
137.             displayBoard(HANGMANPICS, missedLetters, correctLetters, 
secretWord)
138.             print('У вас не осталось попыток!\nПосле '+str(len(missedLetters))
+' ошибок и '+str(len(correctLetters))+'угаданных букв. Загаданное слово:'
+secretWord+'"')
139.             gameIsDone = True
140.     # Спрашиваем, хочет ли игрок сыграть еще раз.
141.
142.     if gameIsDone:
143.         if playAgain():
144.             missedLetters = ''
145.             correctLetters = ''
146.             gameIsDone = False
147.             secretWord = getRandomWord(words)
148.     else:
149.         break
151.         
