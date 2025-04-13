Python Coding Instructions

1. General Guidelines
	•	Python Version: Use Python 3.12+ (or the latest stable version the project supports).
	•	Imports:
        •	Group standard library, third-party, and local imports in separate blocks.
        •	Use absolute imports whenever possible.
        •	Avoid wildcard imports (from module import *).
	•	Dependencies:
        •	Use built-in modules where possible before adding third-party libraries.
        •	Pin exact versions of dependencies when necessary (e.g., in a requirements.txt or pyproject.toml).

2. Naming Conventions
	•	Modules & Packages: Use short, lowercase names (my_module, utils).
	•	Classes: Use CamelCase (MyClass, UserProfile).
	•	Functions & Variables: Use snake_case (calculate_total, user_count).
	•	Constants: Use ALL_CAPS (MAX_BUFFER_SIZE, API_ENDPOINT).
	•	Variables for Unused Returns: Use _ (underscore) for throwaway variables.

3. Code Formatting
	•	Style Checkers: Follow PEP 8 guidelines or equivalent (e.g., use Black for automatic formatting).
	•	Indentation: Use 4 spaces. No tabs.
	•	Line Length: Max 79 or 88 characters (align with your team’s preference or linter config).
	•	Whitespace:
        •	One blank line between top-level definitions (functions/classes).
        •	Separate logical sections of code with blank lines.
	•	String Quotes: Consistent usage of double quotes (" ") project-wide.

4. Readability, Comments and Docstrings
    •	class sections will always be preceeded by 
        #===================================================================================================
        # Foo class
        #===================================================================================================
    •	class sections will always be followed by 
        #===================================================================================================
        # end of Foo class
        #===================================================================================================    
    •	class __init__ sections will always be followed by 
        #===================================================================================================
        # end of Foo class __init__
        #=================================================================================================== 
    •	def sections will always be preceeded by
        #---------------------------------------------------------------------------------------------------
	•	Inline Comments:
        •	Keep them brief and meaningful.
        •	Place them on a new line rather than at the end of a line of code whenever possible.
	•	Docstrings:
        •	For all public modules, functions, classes, and methods, include a docstring following PEP 257.
        •	Use Google-style or reST-style docstrings (whichever your team prefers).
        •	Example (Google-style):

    #---------------------------------------------------------------------------------------------------
    def add_numbers(a: int, b: int) -> int:
        """
        Adds two integers together.
    
        Args:
            a (int): First integer.
            b (int): Second integer.
    
        Returns:
            int: Sum of the two integers.
        """
        return a + b

    #===================================================================================================
    # Foo class
    #===================================================================================================   
    class Foo(): 
        def __init__(self, bar: int):
            self.something = 1
        #===================================================================================================
        # end of Foo class __init__
        #=================================================================================================== 
    #===================================================================================================
    # end of Foo class
    #===================================================================================================   
        

5. Error Handling & Exceptions
	•	Raise Exceptions: Use built-in exceptions where possible (e.g., ValueError, TypeError, RuntimeError).
	•	Custom Exceptions: Define custom exception classes to handle domain-specific errors.
	•	Catch Specific Exceptions: Avoid catching broad exceptions (except Exception:) without a good reason.
	•	Logging:
        •	Use the built-in logging module instead of print statements for production code.
        •	Configure logging levels (e.g., DEBUG, INFO, WARNING, ERROR).

6. Function and Class Design
	•	Single Responsibility: Each function or class method should do exactly one thing.
	•	Short Functions: Keep functions short and focused. If it grows too large, consider refactoring into smaller pieces.
	•	Keyword-Only Arguments: Use keyword-only arguments to improve readability when a function has many parameters (def my_func(*, size=1, shape='circle'):).
	•	Mutable Default Args: Avoid mutable default arguments (e.g., def fn(x=[]): is problematic). Use None and set defaults inside the function body.

7. Testing
	•	Test Framework: Use pytest (or unittest, nose, etc.), but pick one standard for the project.
	•	Directory Structure: Put tests in a dedicated tests/ directory (e.g., project/tests/).
	•	Coverage: Aim for high code coverage. Write unit tests for critical paths and integration tests for multi-module flows.
	•	Naming: Use test_ prefix for test files and functions (e.g., test_utils.py, test_add_numbers).

8. Performance Considerations
	•	Complexity: Prefer readable code over premature micro-optimizations. Optimize only when needed.
	•	Data Structures: Use built-in data structures (list, dict, set, tuple) effectively.
	•	Profiling: Use tools like cProfile or timeit when performance is critical.

9. Project Structure Example        
my_project/
├── src/
│   ├── __init__.py
│   ├── module_one.py
│   ├── module_two.py
│   ├── utils.py
|   └── assets/
├── tests/
│   ├── __init__.py
│   ├── test_module_one.py
│   ├── test_module_two.py
│   └── test_utils.py
├── requirements.txt
├── README.md
└── setup.py (if packaging)

10. GPT Instructions (When Generating Code)
	•	Provide complete Python code within fenced code blocks (```python ... ```).
	•	Include necessary import statements at the top of the code block.
	•	Adhere to the naming and style conventions outlined above.
	•	Explain the core logic in concise inline comments or docstrings where beneficial.
	•	If external libraries are absolutely needed, give a brief rationale for why the library is chosen.
    •	Never change existing formatting 
    •	Never remove existing comments but feel free to add more comments when necessary
    •	Always increment the version number in line 2 with any code change: # file debug version X