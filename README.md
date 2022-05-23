# Shazs24.github.io
Мой сайт
import random
HANGMANPICS = ['''

+---+
 |   |
     |
     |
     |
     |
=========''','''

     +---+
     |   |
     O   |
         |
         |
         |
  =========''','''
 
     +---+
     |   |
     O   |
     |   |
         |
         |
  =========''','''
 
     +---+
     |   |
      O   |
    /|   |
         |
         |
  =========''','''
 
     +---+
     |   |
     O   |
    /|\  |
         |
         |
  =========''','''
 
     +---+
     |   |
     O   |
    /|\  |
    /    |
         |
  =========''','''
 
     +---+
     |   |
     O   |
    /|\  |
    / \  |
         |
  =========''']
 
  words = 'муравей бабуин барсук медведь бобр верблюд 
кошка моллюск кобра пума койот ворона олень собака осел 
утка орел хорек лиса лягушка коза гусь ястреб ящерица лама 
моль обезьяна лось мышь мул тритон выдра сова панда попугай 
голубь питон кролик баран крыса носорог лосось акула змея 
паук аист лебедь тигр жаба форель индейка черепаха ласка 
кит волк вомбат зебра'.split()
 
  def getRandomWord(wordList):
      #Эта функция возвращает случайное слово, которое выбирает из заранее 
созданного списка
      wordIndex = random.randint(0, len(wordList) - 1)
      return wordList[wordIndex]
 
  def displayBoard(HANGMANPICS, missedletters, correctLetters,secretWord):
      print(HANGMANPICS[len(missedLetters)])
      print()
  
      print('Неправильные буквы:', end=' ')
      for letter in missedLetters:
          print(letter, end=' ')
      print()
 
      blanks = '*'*len(secretWord)
      #Заменяем звездочки на правильно угаданные буквы
      for i in range(len(secretWord)):
          if secretWord[i] in correctLetters:
              blanks = blanks[:i] + secretWord[i] + blanks[i+1:]
      #Показываем загаданное слово с пробелами между букв
      for letter in blanks: 
          print(letter, end=' ')
      print()
 
  def getGuess(alreadyGuessed):
      #Возвращает букву, которую ввел игрок. Эта функция проверяет, что введена
 буква, а не какой-то другой символ
      while True:
      print('Введите букву')
      guess = input()
      guess = guess.lower()
      if len(guess) != 1:
          print('Ваша буква:')
      elif guess in alreadyGuessed:
          print ('Вы уже пробовали эту букву. Выберите другую')
      elif guess not in 'ёйцукенгшщзхъфывапролджэячсмитьбю':
          print('Пожалуйста, введите букву кириллицы')
      else:
          return guess

 def playAgain():
     #Эта функция возвращает True если игрок решит сыграть еще раз. 
В противном случае возвращается False
     print('Хотите попробовать еще раз? ("Да" или "Нет")')
     return input().lower().startswith('д')

 print('В И С Е Л И Ц А')
 missedLetters = ''
 correctLetters = ''
 secretWord = getRandomWord(words)
 gameIsDone = False

 while True:
     displayBoard(HANGMANPICS, missedLetters, correctLetters, secretWord)

     #Вычисляем количество букв, которые ввел игрок

     guess = getGuess(missedLetters+correctLetters)

     if guess in secretWord:
         correctLetters = correctLetters + guess

         #Проверка условия победы игрока
         foundAllLetters = True
         for i in range(len(secretWord)):
             if secretWord[i] not in correctLetters:
                 foundAllLetters = False
                break
         if foundAllLetters:
             print('Превосходно! Было загадано слово "'+secretWord+'"
! Вы победили!')

             gameIsDone = True
     else:
         missedLetters = missedLetters+guess

         #Проверка условия проигрыша игрока
         if len(missedLetters) == len(HANGMANPICS) - 1:
             displayBoard(HANGMANPICS, missedLetters, correctLetters, 
secretWord)
             print('У вас не осталось попыток!\nПосле '+str(len(missedLetters))
+' ошибок и '+str(len(correctLetters))+'угаданных букв. Загаданное слово:'
+secretWord+'"')
             gameIsDone = True
    # Спрашиваем, хочет ли игрок сыграть еще раз.

     if gameIsDone:
         if playAgain():
             missedLetters = ''
             correctLetters = ''
             gameIsDone = False
             secretWord = getRandomWord(words)
     else:
         break
