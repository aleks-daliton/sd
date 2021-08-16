# Python library for working with the .sd format for writing service and configuration data (En)

    ####################################################################################################
    #
    # The sd format is designed to store configuration and service data. Text data written according
    # to the rules of the format can be converted into the Python dict format with the help of the 
    # available library. After working with the data or its comments, using the sd-format library, 
    # you can save the data again in .sd format without losing both the comments to the variables and
    # the comments and descriptions to the file itself.
    #
    #
    #
    # The basic concepts and opportunities incorporated in the development of the format:
    #     Maximum accessibility for the perception of complex structured data
    #     Simple and intuitive syntactic rules
    #     Capability of lists as values
    #     Capability of using dictionaries as values
    #     Possibility of multilinear recording of values
    #     Ability to work with comments to the data
    #     Possibility to work with comments to the file
    # --------------------------------------------------------------------------------------------------
    # To convert data stored in .sd format into python dict format, you need to pass the address of the data file:
    #     from sd_format import sd
    #     sd_obj = sd(sd_file_path)
    #     my_dict = sd_obj.decoding_result
    # If you want to save the Python dictionary as an .sd file, pass in the following address
    # pass in the address where the file should be saved as well as the dictionary itself:
    #     from sd_format import sd
    #     sd(sd_file_path, my_dict)
    # You can get detailed information with a description of the syntax and an example of the contents of the sd file in the console via a function call:
    #     from sd_format import sd_info
    #     sd_info()
    #
    ####################################################################################################

    # Example of recording data in .sd format:
        _main_key_0 = 

        # some comment for main_key_1
        main_key_1 =
        .key_1:
        ..key_1_1:  """String with spaces. Possibly other type of quotes."""    # some comment for key_1_1
        ..key_1_2:
        ...key_1_2_1: lue_without_spaces
        ...key_1_2_2:  """triple quoted values can contain characters such as space or comma"""
        .key_2: value_2_1, """last list element"""
        .key_3: a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one
        
        main_key_2 = some_value_will_be_read_as_a_string    # comment for the main_key_2
        main_key_3 = value_3_1, value_3_2, the_long_element_value_over_50_characters_is_placed_last
        main_key_4 = key_4_1: v_4_1_1, key_4_2: in_a_one_line_notation_each_key_has_only_one_str_value
        main_key_5 = key_5_1: v_5_1_1, key_5_2: v_5_2_1, key_5_3: """should be used no more than 3 pair"""
        
        # temporary comment
        main_key_6 =    # comment for the main_key_6
        '''
        Multi-line write of value,
        for main_key_6.
        '''
        
        main_key_7 = """I'm glad to your attention. If bugs are found, write: bug_report@daliton.org"""


    ####################################################################################################
    #
    # After decoding, the data is converted to Python dict:
    #     dict = {
    #         'keys_comments': {
    #             'own_comments': ['Title of .sd file', 'Top description', 'Bottom description'], 
    #             '_main_key_0': {'own_comments': ['', '']}, 
    #             'main_key_1 ': {
    #                 'key_1': {
    #                     'own_comments': ['', ''], 
    #                     'key_1_1': {'own_comments': ['', 'some comment for key_1_1']}, 
    #                     'key_1_2': {
    #                         'own_comments': ['', ''], 
    #                         'key_1_2_1': {'own_comments': ['', '']}, 
    #                         'key_1_2_2': {'own_comments': ['', '']
    #                                       }
    #                     }
    #                 }, 
    #                 'key_2': {'own_comments': ['', '']}, 
    #                 'key_3': {'own_comments': ['', '']}, 
    #                  'own_comments': ['some comment for main_key_1', '']
    #             }, 
    #             'main_key_2 ': {'own_comments': ['', 'comment for the main_key_2']}, 
    #             'main_key_3 ': {'own_comments': ['', '']}, 
    #             'main_key_4 ': {'own_comments': ['', '']}, 
    #             'main_key_5 ': {'own_comments': ['', '']}, 
    #             'main_key_6 ': {'own_comments': ['temporary comment', 'comment for the main_key_6']}, 
    #             'main_key_7 ': {'own_comments': ['', '']}
    #         }, 
    #         '_main_key_0': '', 
    #         'main_key_1 ': {
    #             'key_1': {
    #                 'key_1_1': 'String with spaces. Possibly other type of quotes.', 
    #                 'key_1_2': {
    #                     'key_1_2_1': 'lue_without_spaces', 
    #                     'key_1_2_2': 'triple quoted values can contain characters such as space or comma'
    #                 }
    #             }, 
    #             'key_2': ['value_2_1', 'last list element'], 
    #             'key_3': 'a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one'
    #         }, 
    #         'main_key_2 ': 'some_value_will_be_read_as_a_string', 
    #         'main_key_3 ': ['value_3_1', 'value_3_2', 'the_long_element_value_over_50_characters_is_placed_last'], 
    #         'main_key_4 ': {'key_4_1': 'v_4_1_1', 'key_4_2': 'in_a_one_line_notation_each_key_has_only_one_str_value'}, 
    #         'main_key_5 ': {'key_5_1': 'v_5_1_1', 'key_5_2': 'v_5_2_1', 'key_5_3': 'should be used no more than 3 pair'}, 
    #         'main_key_6 ': 'Multi-line write of value,\nfor main_key_6.', 
    #         'main_key_7 ': "I'm glad to your attention. If bugs are found, write: bug_report@daliton.org"
    #     }
    #
    # --------------------------------------------------------------------------------------------------
    #
    # Rules for writing the contents of a .sd file:
    #   Within the rules, the readability of the data and its structure determines the choice of record type
    #   Textual comments and descriptions are written after the pound sign
    #   Comments written above a line or in a line with a first level key belong
    #   A four space indentation is recommended for comments written on a keyed line
    #   For multiline dictionary entries only comments written on key strings are available
    #   Key names are written using Latin letters, numbers and underscores
    #   Keys start with a letter or underscore and do not contain spaces
    #   The first level keys are followed by an equal sign
    #   In a single line dictionary there is a space before and after the equal sign
    #   In multi-line dictionary entries there is a space before the equal sign
    #   Colon and comma are followed by space
    #   For dictionaries with more than one level of nesting a multi-line entry is used
    #   For multi-line dictionary entries the value of the sub-vocabulary is written in a line under the key
    #   For multi-line dictionary entries, dots are necessary before the key names
    #   The number of dots in front of the nested key names is determined by the nesting depth
    #   Non-multilinear values without a nested dictionary are written on the same line as the key
    #   When writing the list items a comma is necessary between their values
    #   If the dictionary is written as a single-line item, you can write one line for each key
    #   The recommended length of each list value should not exceed 50 characters
    #   Values greater than 50 characters should optimally be the only, or the last
    #   The recommended number of characters of all list items for each key is 100 characters
    #   For a single line entry, after an equal sign it is recommended that the total number of characters does not exceed 100 characters
    #   Values that contain spaces or commas must be enclosed in triple quotes
    #   Values in triple quotes are recommended to be either the only or the last
    #   Only a multi-line entry of a single value is possible for a first level key
    #   For a multi-line entry of a single value you need to use framing lines with triple quotes
    #   Blank lines are added before the superscript comment and after the multiline entry
    #
    ####################################################################################################
    
    
    Translated with www.DeepL.com/Translator (free version)


# Python библиотека для работы с .sd форматом, предназначенным для записи служебных и конфигурационных данных (Ru)
    
    ####################################################################################################
    #
    # Формат sd предназначен для хранения конфигурационных и служебных данных. Данные в текстовом виде, записанные по правилам формата,
    # с помощью имеющейся библиотеки можно приобразовать в формат Python dict. После работы с данными или комментариями к ним, 
    # с помощью библиотеки sd-format, можно вновь сохранить данные в формате .sd, не потеряв как комментарии к переменным,
    # так и комментарии и описания к самому файлу.
    #
    # Основные концепции и возможности, заложенные при разработке формата:
    #     Максимальная доступность для восприятия сложных по структуре данных
    #     Простые и интуитивно понятные синтаксические правила
    #     Возможность использования в качестве значений списков
    #     Возможность использования в качестве значений словарей
    #     Возможность многострочной записи значений
    #     Возможность работы с комментариями к данным
    #     Возможность работы с комментариями к файлу
    # -------------------------------------------------------------------------------------------------
    # Для преобразования данных хранящихся в формате .sd в формат python dict, необходимо передать адрес файла с данными:
    #     from sd_format import sd
    #     sd_obj = sd(sd_file_path)
    #     my_dict = sd_obj.decoding_result
    # Для сохранения словаря Python в файл в формате .sd, в качестве параметров необходимо
    # передать адрес по которому нужно сохранить файл, а также сам словарь:
    #     from sd_format import sd
    #     sd(sd_file_path, my_dict)
    # Подробную информацию с описанием синтаксиса и примером содержимого файла sd всегда можно вывести в консоль
    # через вызов функции:
    #     from sd_format import sd_info
    #     sd_info()
    #
    ####################################################################################################
   

    # Пример записи данных в формате .sd:
        # some comment for main_key_1
        main_key_1 =
        .key_1:
        ..key_1_1:  """String with spaces. Possibly other type of quotes."""    # some comment for key_1_1
        ..key_1_2:
        ...key_1_2_1: lue_without_spaces
        ...key_1_2_2:  """triple quoted values can contain characters such as space or comma"""
        .key_2: value_2_1, """last list element"""
        .key_3: a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one
        
        main_key_2 = some_value_will_be_read_as_a_string    # comment for the main_key_2
        main_key_3 = value_3_1, value_3_2, the_long_element_value_over_50_characters_is_placed_last
        main_key_4 = key_4_1: v_4_1_1, key_4_2: in_a_one_line_notation_each_key_has_only_one_str_value
        main_key_5 = key_5_1: v_5_1_1, key_5_2: v_5_2_1, key_5_3: """should be used no more than 3 pair"""
        
        # temporary comment
        main_key_6 =    # comment for the main_key_6
        '''
        Multi-line write of value,
        for main_key_6.
        '''
        
        main_key_7 = """I'm glad to your attention. If bugs are found, write: bug_report@daliton.org"""


    ####################################################################################################
    #
    # После декодирования данные преобразуются в Python dict:
    #     dict = {
    #         'keys_comments': {
    #             'own_comments': ['Title of .sd file', 'Top description', 'Bottom description'], 
    #             '_main_key_0': {'own_comments': ['', '']}, 
    #             'main_key_1 ': {
    #                 'key_1': {
    #                     'own_comments': ['', ''], 
    #                     'key_1_1': {'own_comments': ['', 'some comment for key_1_1']}, 
    #                     'key_1_2': {
    #                         'own_comments': ['', ''], 
    #                         'key_1_2_1': {'own_comments': ['', '']}, 
    #                         'key_1_2_2': {'own_comments': ['', '']
    #                                       }
    #                     }
    #                 }, 
    #                 'key_2': {'own_comments': ['', '']}, 
    #                 'key_3': {'own_comments': ['', '']}, 
    #                 'own_comments': ['some comment for main_key_1', '']
    #             }, 
    #             'main_key_2 ': {'own_comments': ['', 'comment for the main_key_2']}, 
    #             'main_key_3 ': {'own_comments': ['', '']}, 
    #             'main_key_4 ': {'own_comments': ['', '']}, 
    #             'main_key_5 ': {'own_comments': ['', '']}, 
    #             'main_key_6 ': {'own_comments': ['temporary comment', 'comment for the main_key_6']}, 
    #             'main_key_7 ': {'own_comments': ['', '']}
    #         }, 
    #         '_main_key_0': '', 
    #         'main_key_1 ': {
    #             'key_1': {
    #                 'key_1_1': 'String with spaces. Possibly other type of quotes.', 
    #                 'key_1_2': {
    #                     'key_1_2_1': 'lue_without_spaces', 
    #                     'key_1_2_2': 'triple quoted values can contain characters such as space or comma'
    #                 }
    #             }, 
    #             'key_2': ['value_2_1', 'last list element'], 
    #             'key_3': 'a_good_solution_is_to_place_an_element_value_greater_than_50_characters_as_the_only_one'
    #         }, 
    #         'main_key_2 ': 'some_value_will_be_read_as_a_string', 
    #         'main_key_3 ': ['value_3_1', 'value_3_2', 'the_long_element_value_over_50_characters_is_placed_last'], 
    #         'main_key_4 ': {'key_4_1': 'v_4_1_1', 'key_4_2': 'in_a_one_line_notation_each_key_has_only_one_str_value'}, 
    #         'main_key_5 ': {'key_5_1': 'v_5_1_1', 'key_5_2': 'v_5_2_1', 'key_5_3': 'should be used no more than 3 pair'}, 
    #         'main_key_6 ': 'Multi-line write of value,\nfor main_key_6.', 
    #         'main_key_7 ': "I'm glad to your attention. If bugs are found, write: bug_report@daliton.org"
    #     }
    #
    # --------------------------------------------------------------------------------------------------
    # Правила для записи содержимого файла формата .sd:
    #    В рамках правил, удобство для восприятия данных и их структуры определяет выбор вида записи
    #    Текстовые комментарии и описания записываются после знака решётки
    #    Комментарии, записанные над строкой или в строке с ключом первого уровня, принадлежат ключам
    #    Для комментария, записанного в строке с ключом, рекомендуется четырёх пробельный отступ
    #    Для многострочной записи словарей доступны только комментарии, записанные в строках с ключами
    #    Имена ключей записываются с использованием латинских букв, цифр и знака подчёркивания
    #    Имена ключей начинаются с буквы или с нижнего подчёркивания и не содержат пробелов
    #    После записи ключей первого уровня ставится знак равенства
    #    При однострочной записи словаря, перед и после знака равенства ставится пробел
    #    При многострочной записи словаря, пробел ставится перед знаком равенства
    #    После двоеточия и запятой необходим пробел
    #    Для записи словарей с более чем одним уровнем вложенности используется многострочная запись
    #    Для многострочной записи значение вложенного словаря записывается в строке под ключом
    #    При многострочной записи словарей, перед именами ключей необходимы точки
    #    Количество точек перед именами вложенных ключей определяется глубиной их вложенности
    #    Не многострочные значения без вложенного словаря записываются на одной строке с ключом
    #    При записи элементов списка между их значениями необходима запятая
    #    При однострочной записи словаря, для каждого ключа возможна запись одного строкового значения
    #    Рекомендуемая длина каждого значения списка не должна превышать 50 символов
    #    Значения, превышающие 50 символов, оптимально должны быть единственными, либо последними
    #    Рекомендуемое количество знаков всех элементов списка для каждого ключа составляет 100 знаков
    #    Для однострочной записи, после знака равно рекомендуется суммарная запись не более 100 символов
    #    Значения, в которых есть пробелы или запятые, необходимо заключить в тройные кавычки
    #    Значения в тройных кавычках рекомендуется делать либо единственными, либо последними
    #    Только для ключа первого уровня возможна многострочная запись единственного значения
    #    Для многострочной записи одного значения необходимы обрамляющие строки с тройными кавычками
    #    Перед надстрочным комментарием и после многострочной записи добавляются пустые строки
    #
    ####################################################################################################
