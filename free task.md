class Student:
  def __init__(self, name, surname, gender):
      self.name = name
      self.surname = surname
      self.gender = gender
      self.finished_courses = []
      self.courses_in_progress = []
      self.grades = {}

  def rate_lecturer(self, lecturer, course, grade):
      if isinstance(lecturer, Lecturer) and course in self.courses_in_progress and course in lecturer.courses_attached:
          if course in lecturer.grades:
              lecturer.grades[course].append(grade)
          else:
              lecturer.grades[course] = [grade]
      else:
          return 'Ошибка'

  def average_grade(self):
      total_grades = 0
      total_count = 0
      for grades in self.grades.values():
          total_grades += sum(grades)
          total_count += len(grades)
      return total_grades / total_count if total_count > 0 else 0

  def __str__(self):
      return (f'Имя: {self.name}\n'
              f'Фамилия: {self.surname}\n'
              f'Средняя оценка за домашние задания: {self.average_grade():.2f}\n'
              f'Курсы в процессе изучения: {", ".join(self.courses_in_progress)}\n'
              f'Завершенные курсы: {", ".join(self.finished_courses)}')

  def __lt__(self, other):
      if isinstance(other, Student):
          return self.average_grade() < other.average_grade()
      return NotImplemented

  def __le__(self, other):
      if isinstance(other, Student):
          return self.average_grade() <= other.average_grade()
      return NotImplemented

  def __eq__(self, other):
      if isinstance(other, Student):
          return self.average_grade() == other.average_grade()
      return NotImplemented

  def __gt__(self, other):
      if isinstance(other, Student):
          return self.average_grade() > other.average_grade()
      return NotImplemented

  def __ge__(self, other):
      if isinstance(other, Student):
          return self.average_grade() >= other.average_grade()
      return NotImplemented


class Mentor:
  def __init__(self, name, surname):
      self.name = name
      self.surname = surname
      self.courses_attached = []

  def rate_hw(self, student, course, grade):
      if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
          if course in student.grades:
              student.grades[course].append(grade)
          else:
              student.grades[course] = [grade]
      else:
          return 'Ошибка'


class Lecturer(Mentor):
  def __init__(self, name, surname):
      super().__init__(name, surname)
      self.grades = {}

  def average_grade(self):
      total_grades = 0
      total_count = 0
      for grades in self.grades.values():
          total_grades += sum(grades)
          total_count += len(grades)
      return total_grades / total_count if total_count > 0 else 0

  def __str__(self):
      return (f'Имя: {self.name}\n'
              f'Фамилия: {self.surname}\n'
              f'Средняя оценка за лекции: {self.average_grade():.2f}')

  def __lt__(self, other):
      if isinstance(other, Lecturer):
          return self.average_grade() < other.average_grade()
      return NotImplemented

  def __le__(self, other):
      if isinstance(other, Lecturer):
          return self.average_grade() <= other.average_grade()
      return NotImplemented

  def __eq__(self, other):
      if isinstance(other, Lecturer):
          return self.average_grade() == other.average_grade()
      return NotImplemented

  def __gt__(self, other):
      if isinstance(other, Lecturer):
          return self.average_grade() > other.average_grade()
      return NotImplemented

  def __ge__(self, other):
      if isinstance(other, Lecturer):
          return self.average_grade() >= other.average_grade()
      return NotImplemented


class Reviewer(Mentor):
  def __init__(self, name, surname):
      super().__init__(name, surname)

  def __str__(self):
      return (f'Имя: {self.name}\n'
              f'Фамилия: {self.surname}\n'
              f'У лекторов:')

# Пример использования
student1 = Student('Ruoy', 'Eman', 'your_gender')
student1.courses_in_progress += ['Python', 'Git']
student1.finished_courses += ['Введение в программирование']
student1.grades = {'Python': [9, 10, 8]}

student2 = Student('Alex', 'Johnson', 'your_gender')
student2.courses_in_progress += ['Python', 'Git']
student2.finished_courses += ['Введение в программирование']
student2.grades = {'Python': [10, 9, 9]}

lecturer1 = Lecturer('Some', 'Buddy')
lecturer1.courses_attached += ['Python']
lecturer1.grades = {'Python': [9, 10, 8]}

lecturer2 = Lecturer('Another', 'Lecturer')
lecturer2.courses_attached += ['Python']
lecturer2.grades = {'Python': [10, 9, 9]}

reviewer = Reviewer('Some', 'Reviewer')
reviewer.courses_attached += ['Python']

# Вывод информации
print(reviewer)
print(lecturer1)
print(student1)


# Сравнение студентов
print(student1 > student2)  # Сравнение студентов
print(student1 < student2)  # Сравнение студентов
print(student1 == student2)  # Сравнение студентов

# Сравнение лекторов
print(lecturer1 > lecturer2)  # Сравнение лекторов
print(lecturer1 < lecturer2)  # Сравнение лекторов
print(lecturer1 == lecturer2)  # Сравнение лекторов
