# Library for working with the .sd format designed to store configuration and service data (En)

    ####################################################################################################
    #
    # The main concepts and possibilities inherent in the development of the format:
    #     Maximal accessibility for perception of structurally complex data
    #     Simple and intuitive syntax rules
    #     Ability to write simple dictionaries and lists in one line
    #     Multi-line writing for multidimensional dictionaries
    #     Multi-line writing of string values
    #     Capability of multiline record of long lists
    #     Ability to work with data and file comments
    # --------------------------------------------------------------------------------------------------
    # To convert data stored in .sd format into python dict format, you need to pass the address of the data file:
    #     from sd_format import sd
    #     sd_obj = sd(sd_file_path)
    #     my_dict = sd_obj.decoding_result
    # If you want to save the Python dictionary as an .sd file, pass in the following address
    # pass in the address where the file should be saved as well as the dictionary itself:
    #     from sd_format import sd
    #     sd(sd_file_path, my_dict)
    # You can get detailed information with a description of the syntax and an example of the contents
    # of the sd file in the console via a function call:
    #     from sd_format import sd_info
    #     sd_info()
    #
    ####################################################################################################


    # Пример записи данных в формате .sd (An example of writing data in the .sd format):
    main_key_0 =    # multiline list entry
    ; large_lists_of_values_are_written_into_a_column
    ; lists_containing_nested_lists_are_written_to_a_multi_line_format
    ; lists_written_with_more_than_a_hundred_characters_should_be_written_in_a_multi_line_format
    ;; value_0_4_1
    ;; value_0_4_2
    ;;; value_0_4_3_1
    ;;; value_0_4_3_2
    ;; value_0_4_4
    ; value_0_5
    
    
    # some comment for main_key_1
    main_key_1 =    # multi-line dictionary entry
    . key_1_1:
    .. key_1_1_1:  '''String with spaces. Possibly other type of quotes.'''
    .. key_1_1_2:
    ... key_1_1_2_1: value_without_spaces    # some comment for key_1_1_2_1
    ... key_1_1_2_2:  '''triple quoted values can contain characters such as space or comma'''
    ... key_1_1_2_3: Values_ending_with_a_':'_or_starting_with_a_';'_should_be_enclosed_in_triple_quotes
    . key_1_2: value_1_2_1, '''last list element'''
    . key_1_3: a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one
    
    
    main_key_2 = some_value_will_be_read_as_a_string    # comment for the main_key_2
    main_key_3 = value_3_1, value_3_2, the_long_element_value_over_50_characters_is_placed_last
    main_key_4 = key_4_1: v_4_1_1, key_4_2: in_a_one_line_notation_each_key_has_only_one_str_value
    main_key_5 = key_5_1: v_5_1_1, key_5_2: v_5_2_1, key_5_3: '''should be used no more than 3 pair'''
    
    
    # comment for the main_key_6
    main_key_6 =    # multiline str entry
    """
    Multi-line write of value,
    for main_key_6.
    """
    
    
    _main_key_7 = '''I'm glad to your attention. If bugs are found, write: bug_report@daliton.org'''


    ####################################################################################################
    #
    # After decoding, the data is converted to Python dict:
    #     dict = {
    #       'keys_comments': {
    #           'own_comments':
    #               ['File title',
    #                'Top description of configuration file',
    #                'Bottom part of the descriptions and comments for the configuration file'],
    #           'main_key_0': {
    #               'own_comments':
    #                   ['Пример записи данных в формате .sd (An example of writing data in the .sd format):\n',
    #                    'multiline list entry']
    #           },
    #           'main_key_1': {
    #               'key_1_1': {
    #                   'own_comments': ['', ''],
    #                   'key_1_1_1': {'own_comments': ['', '']},
    #                   'key_1_1_2': {
    #                       'own_comments': ['', ''],
    #                       'key_1_1_2_1': {'own_comments': ['', 'some comment for key_1_1_2_1']},
    #                       'key_1_1_2_2': {'own_comments': ['', '']},
    #                       'key_1_1_2_3': {'own_comments': ['', '']}
    #                   }
    #               },
    #               'key_1_2': {'own_comments': ['', '']},
    #               'key_1_3': {'own_comments': ['', '']},
    #               'own_comments': ['some comment for main_key_1', 'multi-line dictionary entry']
    #           },
    #           'main_key_2': {'own_comments': ['', 'comment for the main_key_2']},
    #           'main_key_3': {'own_comments': ['', '']},
    #           'main_key_4': {'own_comments': ['', '']},
    #           'main_key_5': {'own_comments': ['', '']},
    #           'main_key_6': {'own_comments': ['comment for the main_key_6', 'multiline str entry']},
    #           '_main_key_7': {'own_comments': ['', '']}},
    #       'main_key_0':
    #           ['large_lists_of_values_are_written_into_a_column',
    #            'lists_containing_nested_lists_are_written_to_a_multi_line_format',
    #            'lists_written_with_more_than_a_hundred_characters_should_be_written_in_a_multi_line_format',
    #            ['value_0_4_1', 'value_0_4_2', ['value_0_4_3_1', 'value_0_4_3_2'], 'value_0_4_4'],
    #            'value_0_5'],
    #       'main_key_1': {
    #           'key_1_1': {'key_1_1_1': 'String with spaces. Possibly other type of quotes.',
    #                       'key_1_1_2': {
    #                           'key_1_1_2_1': 'value_without_spaces',
    #                           'key_1_1_2_2': 'triple quoted values can contain characters such as space or comma',
    #                           'key_1_1_2_3': "Values_ending_with_a_':'_or_starting_with_a_';'_should_be_enclosed_in_triple_quotes"
    #                       }
    #            },
    #           'key_1_2': ['value_1_2_1', 'last list element'],
    #           'key_1_3': 'a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one'
    #       },
    #       'main_key_2': 'some_value_will_be_read_as_a_string',
    #       'main_key_3': ['value_3_1', 'value_3_2', 'the_long_element_value_over_50_characters_is_placed_last'],
    #       'main_key_4': {'key_4_1': 'v_4_1_1', 'key_4_2': 'in_a_one_line_notation_each_key_has_only_one_str_value'},
    #       'main_key_5': {'key_5_1': 'v_5_1_1', 'key_5_2': 'v_5_2_1', 'key_5_3': 'should be used no more than 3 pair'},
    #       'main_key_6': 'Multi-line write of value,\nfor main_key_6.',
    #       '_main_key_7': "I'm glad to your attention. If bugs are found, write: bug_report@daliton.org"
    #
    #
    # --------------------------------------------------------------------------------------------------
    #
    # Rules for writing the contents of a .sd file:
    #
    # Basic:
    # Within the rules, the readability of the data and its structure determines the choice of record type
    # The first level keys are followed by an equal sign
    # Key names are written using Latin letters, numbers, periods and underscores
    # Key names begin with a letter, number or underscore and contain no spaces
    # For a single-line entry, after the equal sign a total of 100 characters or less is recommended
    # Values that contain grid sign, spaces or commas must be enclosed in triple quotes
    # Values ending with a colon must be enclosed in triple quotes
    # Values starting with a semicolon must be enclosed in triple quotes
    # It is recommended that values in triple quotes are either the only or the last value
    # Blank lines are added before and after superscript and multiline entries
    # For a multi-line entry, for descriptions of the file, double blank lines are added
    # The following singles or triples are used to mark up the file: #.=:""";'''
    #
    # Writing comments:
    # Text comments and descriptions are written after the grid sign
    # Comments written above a line or in a line with a first level key belong to the keys
    # A four space indentation is recommended for comments written on a keyed line
    # For multi-line dictionary entries only comments written on lines
    #
    # Dictionary entries:
    # For single-line dictionary entries, a space before and after the equal sign
    # For multi-line dictionary entries there is a space before the equal sign
    # After colons and commas a space is necessary
    # For dictionaries with more than one level of nesting a multi-line entry is used
    # For multi-line dictionary entries the value of the sub-vocabulary is written in a line under the key
    # For multi-line dictionary entries, dots are needed before the key names, with one space after
    # The number of dots before a subkey name is determined by the nesting depth
    # Values for a key without a sub-dictionary are written on the same line as the key
    # If you use a one-line dictionary, you can write one string value for each key
    # The recommended number of characters of all list items for each key is 100 characters
    #
    # Writing lists:
    # When recording list items as strings, a comma is required between their values
    # Dictionaries cannot be list items. Passed dictionaries will be converted to string
    # The recommended length of each list value should not exceed 50 characters
    # Values greater than 50 characters should optimally be last
    # For lists longer than 100 characters, multi-line notation should be used
    # For lists that have a nested list, multiline notation should be used
    # In multi-line lists you must not put a comma after each value
    #
    # Multiline notation for a string value
    # Only for a first level key can a multi-line single value be written
    # For a multi-line entry of a single value you need to use framing strings with triple quotes
    # Framing strings with triple quotes are above and below the value, respectively
    #
    #
    ####################################################################################################


# Библиотека для работы с .sd форматом, предназначенным для записи служебных и конфигурационных данных (Ru)

    ####################################################################################################
    #
    # Основные концепции и возможности, заложенные при разработке формата:
    #    Максимальная доступность для восприятия сложных по структуре данных
    #    Простые и интуитивно понятные синтаксические правила
    #    Возможность однострочной записи простых словарей и списков
    #    Возможность многострочной записи многомерных словарей
    #    Возможность многострочной записи строкового значения
    #    Возможность многострочной записи длинных списков
    #    Возможность работы с комментариями к данным и файлу
    # --------------------------------------------------------------------------------------------------
    # Для преобразования данных хранящихся в формате .sd в формат python dict, 
    # необходимо передать адрес файла с данными:
    #     from sd_format import sd
    #     sd_obj = sd(sd_file_path)
    #     my_dict = sd_obj.decoding_result
    # Для сохранения словаря Python в файл в формате .sd, в качестве параметров необходимо
    # передать адрес по которому нужно сохранить файл, а также сам словарь:
    #     from sd_format import sd
    #     sd(sd_file_path, my_dict)
    # Подробную информацию с описанием синтаксиса и примером содержимого файла sd всегда можно вывести 
    # в консоль через вызов функции:
    #     from sd_format import sd_info
    #     sd_info()
    #
    ####################################################################################################


    # Пример записи данных в формате .sd (An example of writing data in the .sd format):
    main_key_0 =    # multiline list entry
    ; large_lists_of_values_are_written_into_a_column
    ; lists_containing_nested_lists_are_written_to_a_multi_line_format
    ; lists_written_with_more_than_a_hundred_characters_should_be_written_in_a_multi_line_format
    ;; value_0_4_1
    ;; value_0_4_2
    ;;; value_0_4_3_1
    ;;; value_0_4_3_2
    ;; value_0_4_4
    ; value_0_5
    
    
    # some comment for main_key_1
    main_key_1 =    # multi-line dictionary entry
    . key_1_1:
    .. key_1_1_1:  '''String with spaces. Possibly other type of quotes.'''
    .. key_1_1_2:
    ... key_1_1_2_1: value_without_spaces    # some comment for key_1_1_2_1
    ... key_1_1_2_2:  '''triple quoted values can contain characters such as space or comma'''
    ... key_1_1_2_3: Values_ending_with_a_':'_or_starting_with_a_';'_should_be_enclosed_in_triple_quotes
    . key_1_2: value_1_2_1, '''last list element'''
    . key_1_3: a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one
    
    
    main_key_2 = some_value_will_be_read_as_a_string    # comment for the main_key_2
    main_key_3 = value_3_1, value_3_2, the_long_element_value_over_50_characters_is_placed_last
    main_key_4 = key_4_1: v_4_1_1, key_4_2: in_a_one_line_notation_each_key_has_only_one_str_value
    main_key_5 = key_5_1: v_5_1_1, key_5_2: v_5_2_1, key_5_3: '''should be used no more than 3 pair'''
    
    
    # comment for the main_key_6
    main_key_6 =    # multiline str entry
    """
    Multi-line write of value,
    for main_key_6.
    """
    
    
    _main_key_7 = '''I'm glad to your attention. If bugs are found, write: bug_report@daliton.org'''


    ####################################################################################################
    #
    # После парсинга данные преобразуются в Python dict:
    #     dict = {
    #       'keys_comments': {
    #           'own_comments':
    #               ['File title',
    #                'Top description of configuration file',
    #                'Bottom part of the descriptions and comments for the configuration file'],
    #           'main_key_0': {
    #               'own_comments':
    #                   ['Пример записи данных в формате .sd (An example of writing data in the .sd format):\n',
    #                    'multiline list entry']
    #           },
    #           'main_key_1': {
    #               'key_1_1': {
    #                   'own_comments': ['', ''],
    #                   'key_1_1_1': {'own_comments': ['', '']},
    #                   'key_1_1_2': {
    #                       'own_comments': ['', ''],
    #                       'key_1_1_2_1': {'own_comments': ['', 'some comment for key_1_1_2_1']},
    #                       'key_1_1_2_2': {'own_comments': ['', '']},
    #                       'key_1_1_2_3': {'own_comments': ['', '']}
    #                   }
    #               },
    #               'key_1_2': {'own_comments': ['', '']},
    #               'key_1_3': {'own_comments': ['', '']},
    #               'own_comments': ['some comment for main_key_1', 'multi-line dictionary entry']
    #           },
    #           'main_key_2': {'own_comments': ['', 'comment for the main_key_2']},
    #           'main_key_3': {'own_comments': ['', '']},
    #           'main_key_4': {'own_comments': ['', '']},
    #           'main_key_5': {'own_comments': ['', '']},
    #           'main_key_6': {'own_comments': ['comment for the main_key_6', 'multiline str entry']},
    #           '_main_key_7': {'own_comments': ['', '']}},
    #       'main_key_0':
    #           ['large_lists_of_values_are_written_into_a_column',
    #            'lists_containing_nested_lists_are_written_to_a_multi_line_format',
    #            'lists_written_with_more_than_a_hundred_characters_should_be_written_in_a_multi_line_format',
    #            ['value_0_4_1', 'value_0_4_2', ['value_0_4_3_1', 'value_0_4_3_2'], 'value_0_4_4'],
    #            'value_0_5'],
    #       'main_key_1': {
    #           'key_1_1': {'key_1_1_1': 'String with spaces. Possibly other type of quotes.',
    #                       'key_1_1_2': {
    #                           'key_1_1_2_1': 'value_without_spaces',
    #                           'key_1_1_2_2': 'triple quoted values can contain characters such as space or comma',
    #                           'key_1_1_2_3': "Values_ending_with_a_':'_or_starting_with_a_';'_should_be_enclosed_in_triple_quotes"
    #                       }
    #            },
    #           'key_1_2': ['value_1_2_1', 'last list element'],
    #           'key_1_3': 'a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one'
    #       },
    #       'main_key_2': 'some_value_will_be_read_as_a_string',
    #       'main_key_3': ['value_3_1', 'value_3_2', 'the_long_element_value_over_50_characters_is_placed_last'],
    #       'main_key_4': {'key_4_1': 'v_4_1_1', 'key_4_2': 'in_a_one_line_notation_each_key_has_only_one_str_value'},
    #       'main_key_5': {'key_5_1': 'v_5_1_1', 'key_5_2': 'v_5_2_1', 'key_5_3': 'should be used no more than 3 pair'},
    #       'main_key_6': 'Multi-line write of value,\nfor main_key_6.',
    #       '_main_key_7': "I'm glad to your attention. If bugs are found, write: bug_report@daliton.org"
    #
    #
    # --------------------------------------------------------------------------------------------------
    #
    # Правила для записи содержимого файла формата .sd:
    #
    #    Основное:
    #    В рамках правил, удобство для восприятия данных и их структуры определяет выбор вида записи
    #    После записи ключей первого уровня ставится знак равенства
    #    Имена ключей записываются с использованием латинских букв, цифр, точки и знака подчёркивания
    #    Имена ключей начинаются с буквы, цифры или с нижнего подчёркивания и не содержат пробелов
    #    Для однострочной записи, после знака равно рекомендуется суммарная запись не более 100 символов
    #    Значения, в которых есть решётка, пробелы или запятые, необходимо заключить в тройные кавычки
    #    Значения, заканчивающиеся двоеточием, необходимо заключить в тройные кавычки
    #    Значения, начинающиеся с точки с запятой, необходимо заключить в тройные кавычки
    #    Значения в тройных кавычках рекомендуется делать либо единственными, либо последними
    #    Перед и после надстрочного комментария и многострочной записи добавляются пустые строки
    #    Для многострочной записи, после или перед описаниями к файлу, добавляются двойные пустые строки
    #    Для разметки файла используются следующие одиночные или тройные знаки: #.=:""";'''
    #
    #    Запись комментариев:
    #    Текстовые комментарии и описания записываются после знака решётки
    #    Комментарии, записанные над строкой или в строке с ключом первого уровня, принадлежат ключам
    #    Для комментария, записанного в строке с ключом, рекомендуется четырёх пробельный отступ
    #    Для многострочной записи словарей ключам доступны только комментарии, записанные в строках
    #
    #    Запись словарей:
    #    При однострочной записи словаря, перед и после знака равенства ставится пробел
    #    При многострочной записи словаря, пробел ставится перед знаком равенства
    #    После двоеточия и запятой необходим пробел
    #    Для записи словарей с более чем одним уровнем вложенности используется многострочная запись
    #    Для многострочной записи значение вложенного словаря записывается в строке под ключом
    #    При многострочной записи словарей, перед именами ключей необходимы точки с одним пробелом после
    #    Количество точек перед именами вложенных ключей определяется глубиной их вложенности
    #    Значения для ключа без вложенного словаря записываются на одной строке с ключом
    #    При однострочной записи словаря, для каждого ключа возможна запись одного строкового значения
    #    Сумма символов для однострочной записи словаря составляет 100 знаков
    #
    #    Запись списков:
    #    При однострочной записи элементов списка между их значениями необходима запятая
    #    Словари не могут быть элементами списка. Переданные словари будут приведены к строковому виду
    #    Рекомендуемая длина каждого значения списка не должна превышать 50 символов
    #    Значения, превышающие 50 символов, оптимально должны быть последними
    #    Для списков длинной более 100 знаков, нужно использовать многострочную запись
    #    Для списков имеющих вложенный список, нужно использовать многострочную запись
    #    При многострочной записи списков, запятая после каждого значения не ставится
    #
    #    Многострочная запись строкового значения:
    #    Только для ключа первого уровня возможна многострочная запись единственного значения
    #    Для многострочной записи одного значения необходимы обрамляющие строки с тройными кавычками
    #    Обрамляющие строки с тройными кавычками находятся соответственно над и под значением
    #
    ####################################################################################################

Translated with www.DeepL.com/Translator (free version)
