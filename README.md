
    #include "MainClass.h"

    #include <iostream>
	
    #include <string>
	
    #include <fstream>

    void MainClass::main(std::vector<std::wstring> &args)
    {

	// 1 задание
	std::wcout << L"Проверка ответа на задание 1:" << std::endl;
	// Загрузка в строку символов из входного файла задания 1
	std::wstring s1 = std::wstring(Files::readAllBytes(Paths->get(L"task1")));
	// Разделить полученную строку по пробелам на массив строк (слова)
	std::vector<std::wstring> ss = s1.split(L" ");
	// Длина самого короткого слова
	int min = 255;
	// Проходим по всем словам
	for (auto s : ss)
	{
		// Считываем длину текущего слова
		int temp = s.length();
		// Сравниваем с длиной самого короткого слова
		if (temp < min)
		{
			//если оно ещё меньше, то теперь это слово минимальное
			min = temp;
		}
	}
	// Выводим минимальное
	std::wcout << min << std::endl;

	// 2 задание
	std::wcout << L"Проверка ответа на задание 2:" << std::endl;
	// Методом буфферизированного чтения считываем строки с файла задания 2
	FileReader tempVar(L"task2");
	BufferedReader *reader2 = new BufferedReader(&tempVar);
	// считываем первую строку
	std::wstring c2 = reader2->readLine();
	// считываем вторую строку
	std::wstring s2 = reader2->readLine();
	// разбиваем вторую строку на слова
	std::vector<std::wstring> ss2 = s2.split(L" ");
	// проходим по всем словам второй строки
	for (auto s : ss2)
	{
		// если слово начинается на букву первой строки
		if (s.startsWith(c2))
		{
			// выводим его на экран
			std::wcout << s << std::endl;
		}
	}
	// очищаем считыватель
	reader2->close();

	// 3 задание
	std::wcout << L"Проверка ответа на задание 3:" << std::endl;
	// Загрузка в строку символов из входного файла задания 3
	std::wstring s3 = std::wstring(Files::readAllBytes(Paths->get(L"task3")));
	// разбиение строки по пробелам
	std::vector<std::wstring> ss3 = s3.split(L" ");
	// конструктор будущей строки
	StringBuilder *sb3 = new StringBuilder();
	// проходим по всем частям строки
	for (auto s : ss3)
	{
		// если содержит точку
		if (s.startsWith(L"."))
		{
			// заменяем на 3 точки
			s = L"...";
			// добавляем в будущую строку
			sb3->append(s + L" ");
		}
		// если не точка добавляем без изменений
		else
		{
			sb3->append(s + L" ");
		}
	}
	// выводим итоговую строку
	std::wcout << sb3->toString() << std::endl;

	// 4 задание
	std::wcout << L"Проверка задания 4 в файле task4_output" << std::endl;
	//// Методом буфферизированного чтения считываем строки с входного файла задания 4
	FileReader tempVar2(L"task4_input");
	BufferedReader *reader4 = new BufferedReader(&tempVar2);
	// Используем конструктор записи текстовых файлов для записи в выходной файл задания 4
	FileWriter *writer4 = new FileWriter(L"task4_output");
	// Считываем из входного файла первую строку
	std::wstring s4 = reader4->readLine();
	// Пока не конец входного файла
	while (s4 != L"")
	{
		// записываем в выходной файл текущую строку
		// через пробел ее длин и переносим каретку на следующую строку
		writer4->write(s4 + L" " + std::to_wstring(s4.length()) + StringHelper::toString(L'\n'));
		// считываем из входного файла следующую строку
		s4 = reader4->readLine();
	}
	// выносим всё записанное в файл
	writer4->flush();
	// закрываем для очистки памяти
	writer4->close();
	reader4->close();

	// 5 задание
	std::wcout << L"Проверка задания 5 в файле task5_output" << std::endl;
	//// Методом буфферизированного чтения считываем строки с входного файла задания 5
	FileReader tempVar3(L"task5_input");
	BufferedReader *reader5 = new BufferedReader(&tempVar3);
	// считываем первую строку входного файла
	std::wstring s5 = reader5->readLine();
	// находим в ней 2 числа
	std::vector<std::wstring> ss5 = s5.split(L"\\D+");
	// присваиваем их по порядку
	int k1 = std::stoi(ss5[0]);
	int k2 = std::stoi(ss5[1]);
	// запись в выходной файл задания 5
	FileWriter *writer5 = new FileWriter(L"task5_output");
	// создаем список строк
	std::vector<std::wstring> list5;
	//считываем вторую строку входного файла
	s5 = reader5->readLine();
	// пока в файле есть строки
	while (s5 != L"")
	{
		// добавляем текущую строку в список
		list5.push_back(s5);
		// считываем следующую строку
		s5 = reader5->readLine();
	}
	// проходим по интервалу заданному числами из первой строки
	for (int i = k1; i <= k2; i++)
	{
		// записать текущую строку с текущим индексом (-1 т.к. индексация в списке идет с 0)
		writer5->write(list5[i - 1] + StringHelper::toString(L'\n'));
	}
	// вынести все в выходной файл задания 5
	writer5->flush();
	// закрыть для очистки памяти
	writer5->close();
	reader5->close();


	// 6 задание
	std::wcout << L"Проверка задания 6 в файле task6_output" << std::endl;
	//// Методом буфферизированного чтения считываем строки с входного файла задания 6
	FileReader tempVar4(L"task6_input");
	BufferedReader *reader6 = new BufferedReader(&tempVar4);
	// список всех строк входного файла
	std::vector<std::wstring> list6;
	// считываем первую строку
	std::wstring s6 = reader6->readLine();
	// пока в файле ещё есть строки
	while (s6 != L"")
	{
		// добавляем их в список
		list6.push_back(s6);
		s6 = reader6->readLine();
	}
	// констурктор выходного файла
	FileWriter *writer6 = new FileWriter(L"task6_output");
	// идем по всему списку строк
	for (auto s : list6)
	{
		// если есть строка с пробелом
		if (s.contains(L" "))
		{
			// добавляем ее в выходной файл
			writer6->write(s + L'\n');
		}
	}
	// выгружаем в выходной файл и закрываем
	writer6->flush();
	writer6->close();
	reader6->close();

	// 7 задание
	std::wcout << L"Проверка ответа на задание 7:" << std::endl;
	// предложение
	std::wstring s71 = L"one, two, three";
	// номера символов
	std::wstring s72 = L"3 8";
	//переводим их из строкового формата в целочисленный
	// получая символы по индексу первого(0) и третьего(2) (без пробела) элементов строки
	int s7 = Character::getNumericValue(s72[0]);
	int k7 = Character::getNumericValue(s72[2]);
	//В конструктор строк помещаем предложение
	StringBuilder *sb7 = new StringBuilder(s71);
	// Вставляем букву s на место k
	// получая символ по индексу s-1, т.к. индексация в конструкторе начинается с 0
	sb7->insert(k7, s71[s7 - 1]);
	// удаляем s с ее прежнего места
	sb7->deleteCharAt(s7 - 1);
	// выводим результат
	std::wcout << sb7->toString() << std::endl;

	// 8 задание
	std::wcout << L"Проверка ответа на задание 8:" << std::endl;
	// входное предложение
	std::wstring s8 = L"How many words?";
	// разделяем по пробелам на слова
	std::vector<std::wstring> ss8 = s8.split(L" ");
	// если число слов больше трех
	if (ss8.size() > 3)
	{
		// выводим yes
		std::wcout << L"yes" << std::endl;
	}
	else
	{
		// если меньше трех, то no
		std::wcout << L"no" << std::endl;
	}

	// 9 задание
	std::wcout << L"Проверка ответа на задание 9:" << std::endl;
	// входное слово
	std::wstring s9 = L"word";
	// получаем длину слова
	int length = s9.length();
	// помещаем слово в конструктор строк
	StringBuilder *sb9 = new StringBuilder(s9);
	// по количеству длины слова
	for (int i = 0; i < length; i++)
	{
		// вставляем * в начало
		sb9->insert(0,L"*");
		// вставляем * в конец
		sb9->insert(length + i + 1,L"*");
	}
	// выводим результат на экран
	std::wcout << sb9->toString() << std::endl;

	// 10 задание
	std::wcout << L"Проверка ответа на задание 10:" << std::endl;
	// входные буквы
	std::wstring s101 = L"abcd";
	// строка, в которой будет происходить поиск букв
	std::wstring s102 = L"aaccddhklm";
	// для каждого символа первой строки
	for (auto c : std::vector<wchar_t>(s101.begin(), s101.end()))
	{
		// проверяем есть ли во второй строке этот символ по индексу
		// если символа нет, индекс этого символа во второй строке будет равен -1
		// соответсвтенно на экран выведется false
		// если есть, то true
		std::wcout << (s102.find(c) != std::wstring::npos) << L" ";
	}
	// Перенос строки
	std::wcout << std::endl;

	// 11 задание
	std::wcout << L"Проверка ответа на задание 11:" << std::endl;
	// входная строка
	std::wstring s11 = L"AacИИ1фcфBBqQrc";
	// структура данных списка без повторений значений
	std::unordered_set<wchar_t> set11 = std::unordered_set();
	// добавляем в список Set все символы из строки приведенные к нижнему регистру
	for (auto c : StringHelper::toLower(s11).toCharArray())
	{
		// в список будет добавлены только уникальные символы без повторенийа
			set11.insert(static_cast<std::optional<wchar_t>>(c));
	}
	// выведем размер списка, т.е. сколько всего уникальных букв
	std::wcout << set11.size() << std::endl;

	// 12 задание
	std::wcout << L"Проверка ответа на задание 12:" << std::endl;
	// входная строка
	std::wstring s12 = L"1 - one, 2 - two, 3 - three";
	// максимальная цифра
	int max = -1;
	// проходим по каждому символу строки
	for (auto c : std::vector<wchar_t>(s12.begin(), s12.end()))
	{
		//если символ - цифра
		if (std::isdigit(c) == true)
		{
			// переводим в целое число
			int tmp = Character::getNumericValue(c);
			// если текущая цифра больше предыдущей максимальной
			if (tmp > max)
			{
				// то теперь она максимальная
				max = tmp;
			}
		}
	}
	// выводим максимальную цифру
	std::wcout << max << std::endl;

	delete sb9;
	delete sb7;
	delete writer6;
	delete reader6;
	delete writer5;
	delete reader5;
	delete writer4;
	delete reader4;
	delete sb3;
	delete reader2;
	}
