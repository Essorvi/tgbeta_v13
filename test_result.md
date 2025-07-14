#====================================================================================================
# START - Testing Protocol - DO NOT EDIT OR REMOVE THIS SECTION
#====================================================================================================

# THIS SECTION CONTAINS CRITICAL TESTING INSTRUCTIONS FOR BOTH AGENTS
# BOTH MAIN_AGENT AND TESTING_AGENT MUST PRESERVE THIS ENTIRE BLOCK

# Communication Protocol:
# If the `testing_agent` is available, main agent should delegate all testing tasks to it.
#
# You have access to a file called `test_result.md`. This file contains the complete testing state
# and history, and is the primary means of communication between main and the testing agent.
#
# Main and testing agents must follow this exact format to maintain testing data. 
# The testing data must be entered in yaml format Below is the data structure:
# 
## user_problem_statement: {problem_statement}
## backend:
##   - task: "Task name"
##     implemented: true
##     working: true  # or false or "NA"
##     file: "file_path.py"
##     stuck_count: 0
##     priority: "high"  # or "medium" or "low"
##     needs_retesting: false
##     status_history:
##         -working: true  # or false or "NA"
##         -agent: "main"  # or "testing" or "user"
##         -comment: "Detailed comment about status"
##
## frontend:
##   - task: "Task name"
##     implemented: true
##     working: true  # or false or "NA"
##     file: "file_path.js"
##     stuck_count: 0
##     priority: "high"  # or "medium" or "low"
##     needs_retesting: false
##     status_history:
##         -working: true  # or false or "NA"
##         -agent: "main"  # or "testing" or "user"
##         -comment: "Detailed comment about status"
##
## metadata:
##   created_by: "main_agent"
##   version: "1.0"
##   test_sequence: 0
##   run_ui: false
##
## test_plan:
##   current_focus:
##     - "Task name 1"
##     - "Task name 2"
##   stuck_tasks:
##     - "Task name with persistent issues"
##   test_all: false
##   test_priority: "high_first"  # or "sequential" or "stuck_first"
##
## agent_communication:
##     -agent: "main"  # or "testing" or "user"
##     -message: "Communication message between agents"

# Protocol Guidelines for Main agent
#
# 1. Update Test Result File Before Testing:
#    - Main agent must always update the `test_result.md` file before calling the testing agent
#    - Add implementation details to the status_history
#    - Set `needs_retesting` to true for tasks that need testing
#    - Update the `test_plan` section to guide testing priorities
#    - Add a message to `agent_communication` explaining what you've done
#
# 2. Incorporate User Feedback:
#    - When a user provides feedback that something is or isn't working, add this information to the relevant task's status_history
#    - Update the working status based on user feedback
#    - If a user reports an issue with a task that was marked as working, increment the stuck_count
#    - Whenever user reports issue in the app, if we have testing agent and task_result.md file so find the appropriate task for that and append in status_history of that task to contain the user concern and problem as well 
#
# 3. Track Stuck Tasks:
#    - Monitor which tasks have high stuck_count values or where you are fixing same issue again and again, analyze that when you read task_result.md
#    - For persistent issues, use websearch tool to find solutions
#    - Pay special attention to tasks in the stuck_tasks list
#    - When you fix an issue with a stuck task, don't reset the stuck_count until the testing agent confirms it's working
#
# 4. Provide Context to Testing Agent:
#    - When calling the testing agent, provide clear instructions about:
#      - Which tasks need testing (reference the test_plan)
#      - Any authentication details or configuration needed
#      - Specific test scenarios to focus on
#      - Any known issues or edge cases to verify
#
# 5. Call the testing agent with specific instructions referring to test_result.md
#
# IMPORTANT: Main agent must ALWAYS update test_result.md BEFORE calling the testing agent, as it relies on this file to understand what to test next.

#====================================================================================================
# END - Testing Protocol - DO NOT EDIT OR REMOVE THIS SECTION
#====================================================================================================


#====================================================================================================
# Testing Data - Main Agent and testing sub agent both should log testing data below this section
#====================================================================================================

user_problem_statement: "Полный ребрендинг бота с УЗРИ на SlitInfo и удаление избыточной кнопки 'Купить поиск'"

backend:
  - task: "Изменить BOT_USERNAME в .env файле"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/.env"
    stuck_count: 0
    priority: "high"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Изменен BOT_USERNAME с 'search1_test_bot' на 'SlitInfo_bot' в .env файле"
  
  - task: "Изменить REQUIRED_CHANNEL в .env файле"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/.env"
    stuck_count: 0
    priority: "high"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Изменен REQUIRED_CHANNEL с '@uzrisebya' на '@SlitInfo' в .env файле"
  
  - task: "Обновить название сервиса во всех файлах"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/server.py"
    stuck_count: 0
    priority: "high"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Заменены все упоминания 'УЗРИ' на 'SlitInfo' в названиях, описаниях и API title"
  
  - task: "Удалить избыточную кнопку 'Купить поиск'"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/server.py"
    stuck_count: 0
    priority: "high"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Удалена кнопка 'Купить поиск (25₽)' из главного меню и меню баланса, так как поиск автоматически списывается с баланса. Также удален обработчик buy_single_search"
  
  - task: "Унификация главного меню"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/server.py"
    stuck_count: 0
    priority: "medium"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Заменена дублированная hardcoded клавиатура в show_main_menu на использование функции create_main_menu"

  - task: "Обновить все упоминания каналов и ссылок"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/server.py"
    stuck_count: 0
    priority: "high"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Заменены все упоминания '@uzrisebya' на '@SlitInfo' в сообщениях пользователям"
  
  - task: "Обновить реферальную систему"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/server.py"
    stuck_count: 0
    priority: "high"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Реферальная система обновлена: условие подписки изменено на @SlitInfo, ссылки теперь ведут на SlitInfo_bot"
  
  - task: "Обновить платежные описания"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend/server.py"
    stuck_count: 0
    priority: "high"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Обновлены описания платежей с 'Пополнение баланса УЗРИ' на 'Пополнение баланса SlitInfo'"
  
  - task: "Обновить тестовые файлы"
    implemented: true
    working: true
    file: "/app/telegram_bot/backend_test.py, /app/telegram_bot/backend_test_new.py, /app/telegram_bot/admin_broadcast_test.py, /app/telegram_bot/backend_test_critical.py"
    stuck_count: 0
    priority: "medium"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Обновлены все тестовые файлы с новыми названиями и API endpoint проверками"

frontend:
  - task: "Обновить документацию"
    implemented: true
    working: true
    file: "/app/telegram_bot/README.md"
    stuck_count: 0
    priority: "medium"
    needs_retesting: false
    status_history:
      - working: true
        agent: "main"
        comment: "Полностью обновлена документация с новым названием бота и каналом"

metadata:
  created_by: "main_agent"
  version: "2.1"
  test_sequence: 0
  run_ui: false

test_plan:
  current_focus:
    - "Полный ребрендинг и оптимизация завершены"
  stuck_tasks: []
  test_all: false
  test_priority: "high_first"

agent_communication:
  - agent: "main"
    message: "Выполнен полный ребрендинг бота с УЗРИ на SlitInfo и удалена избыточная кнопка 'Купить поиск'. Теперь пользователи могут сразу делать поиск если у них есть баланс ≥25₽, а при недостатке средств система автоматически предложит пополнить баланс. Это улучшает пользовательский опыт и убирает лишние шаги."