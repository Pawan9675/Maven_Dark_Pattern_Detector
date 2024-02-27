# Team MAVEN
## Dark Pattern Detector
### What is this project all about?
- This project is a tool which is used to detects the dark pattern in the web page and highlights it.
- It helps users recognize patterns that may lead to unintentional actions.
- Such as misleading information, hiding costs, or unwanted subscription.
- This tool aims to promote transprancy and protect user from engaging in actions they did not intend to take due to deceptive design practices.

### What things does it detect?

#### Countdown dark pattern
- To identify countdown dark patterns the following tools are used
  - Chrome storage API
    - This tool is utilized to store and retrieve data within the browser. It's used to remember if the extension should be active or inactive on different tabs, helping in managing the countdown detection process.
  - Content scripts
    - These are scripts that run within web pages and can interact with their content. They are employed to scan web pages for countdown dark patterns, enabling the extension to detect when these patterns are present.
  - Message passing
    - This mechanism enables communication between different parts of the extension, such as between content scripts and background scripts. It's used to relay information about detected countdown dark patterns from content scripts to other components of the extension for further processing
  - Chrome Tab API
    - This API allows the extension to manipulate tabs in the browser. It's used to monitor tab events, such as when tabs are opened, updated, or closed, which helps in coordinating the detection of countdown dark patterns across different tabs.
  - Chrome Runtime API
    - This API is responsible for managing the behavior of the extension and facilitating communication between its various components. It plays a role in handling messages exchanged between different scripts and components involved in detecting countdown dark patterns.

#### Scarcity
- The files use a simple logic to identify scarcity dark patterns
  - Counting visible dark patterns: 
    - The extension counts the number of visible patterns on a webpage. It uses basic logic to detect and count these patterns. This counting process is not based on any complex algorithm but rather on straightforward logic to identify and tally visible patterns.
  - Comparison and decision-making
    - After counting the visible patterns, the extension compares the count to determine if there are any patterns present. If there are patterns, it marks the extension as active. If there are no patterns, it marks the extension as inactive. This decision-making process is based on simple comparisons

### What is the algorithm used for detection of the pattern?

#### The regular expression (regex) 
- This is a pattern identifier in javascript searches for the following combinations/ keywords
- Matches one or more digits (number).
- Matches zero or more whitspaces or character
- Matches any of the specific terms such as customer, client, buyer etc.
- Matches combination of words such as also bought, purchased, ordered
- These comments are indicative of the presence of social proof element

#### Detection Function
- The detection function is the core logic for identifying countdown patterns.
- It uses regular expressions (reg and regBad) to match and filter countdown-like text patterns.
- It compares the current state (node.innerText) and the old state (nodeOld.innerText) of a DOM element.
- It checks for valid countdown matches and ensures that the counts are decreasing over time.
- If a countdown is detected, the function returns true, otherwise, it returns false.

#### Regular Expressions
- reg: Regular expression for a typical countdown format.
- regBad: Regular expression to filter out false positives by checking for too many numbers in the text.

#### Matching and Comparison
- The code extracts and compares numerical values from the countdown text in the current and old states.
- It ensures that the numbers decrease over time, indicating an elapsing countdown.

#### Accessing Text Content
- node.innerText and nodeOld.innerText are used to access the textual content of the DOM elements represented by node and nodeOld, respectively. 
- This text content is then used for comparison to detect changes.

#### Manipulating Classes
- The className property is used to associate a CSS class with the detected countdown pattern. 
- This could be useful for styling or further identification of elements with this pattern.

#### DOM Manipulation for Countdown Detection
- The code examines the text content of DOM elements (node and nodeOld) to identify countdown patterns. 
- It uses the DOM to retrieve and compare the text content, essential for the countdown detection logic.

#### Pattern Information
- The infoUrl and info properties likely point to external resources or information related to the countdown pattern. 
- The DOM can be used to create links or display information dynamically based on these properties.

In summary, the DOM is crucial in this code for accessing and manipulating the content of web pages, which is essential for detecting countdown patterns. The provided code operates in a browser environment, and the DOM is a fundamental part of web development for interacting with HTML documents.