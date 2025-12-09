{
  "SurveyEntry": {
    "SurveyID": "SV_AIStudyPostTask001",
    "SurveyName": "AI Study Post-Task Questionnaire",
    "SurveyStatus": "Inactive",
    "SurveyLanguage": "EN"
  },
  "SurveyElements": [
    {
      "Element": "FL",
      "PrimaryAttribute": "FL_1",
      "Payload": {
        "FlowID": "FL_1",
        "Type": "Root",
        "Flow": [
          { "Type": "Block", "ID": "BL_Load" },
          { "Type": "Block", "ID": "BL_Motivation" },
          { "Type": "Block", "ID": "BL_Anxiety" },
          { "Type": "Block", "ID": "BL_SUS" },
          { "Type": "Block", "ID": "BL_Comprehension" },
          { "Type": "Block", "ID": "BL_AIHelp", "Description": "Shown only to AI-assisted group" },
          { "Type": "Block", "ID": "BL_Reflection" }
        ]
      }
    },

    /* -------------------- BLOCK: Cognitive Load -------------------- */
    {
      "Element": "BL",
      "PrimaryAttribute": "BL_Load",
      "Payload": {
        "BlockID": "BL_Load",
        "Description": "Cognitive Load",
        "BlockElements": [
          { "Type": "Question", "QuestionID": "Q_Load" }
        ]
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Load",
      "Payload": {
        "QuestionID": "Q_Load",
        "QuestionText": "Please rate the following statements about your experience performing the search task.",
        "QuestionType": "Matrix",
        "Selector": "Likert",
        "SubSelector": "SingleAnswer",
        "Choices": {
          "1": {"Display": "The search task was complex."},
          "2": {"Display": "The search task required a great deal of mental effort."},
          "3": {"Display": "The interface was confusing."},
          "4": {"Display": "I had to exert effort dealing with unclear parts of the task."},
          "5": {"Display": "I invested mental effort evaluating article relevance."},
          "6": {"Display": "I tried to understand how the article related to the research question."}
        },
        "Answers": {
          "1": {"Display": "Strongly Disagree"},
          "2": {"Display": "Disagree"},
          "3": {"Display": "Neutral"},
          "4": {"Display": "Agree"},
          "5": {"Display": "Strongly Agree"}
        }
      }
    },

    /* -------------------- BLOCK: Motivation -------------------- */
    {
      "Element": "BL",
      "PrimaryAttribute": "BL_Motivation",
      "Payload": {
        "BlockID": "BL_Motivation",
        "Description": "Motivation",
        "BlockElements": [
          { "Type": "Question", "QuestionID": "Q_Motivation" }
        ]
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Motivation",
      "Payload": {
        "QuestionID": "Q_Motivation",
        "QuestionText": "Please indicate how much you agree with the following statements.",
        "QuestionType": "Matrix",
        "Selector": "Likert",
        "SubSelector": "SingleAnswer",
        "Choices": {
          "1": {"Display": "I tried to understand the task deeply."},
          "2": {"Display": "I made an effort to ensure the article matched the research question."},
          "3": {"Display": "I found the task engaging."},
          "4": {"Display": "I felt motivated to complete the task well."}
        },
        "Answers": {
          "1": {"Display": "Strongly Disagree"},
          "2": {"Display": "Disagree"},
          "3": {"Display": "Neutral"},
          "4": {"Display": "Agree"},
          "5": {"Display": "Strongly Agree"}
        }
      }
    },

    /* -------------------- BLOCK: Anxiety -------------------- */
    {
      "Element": "BL",
      "PrimaryAttribute": "BL_Anxiety",
      "Payload": {
        "BlockID": "BL_Anxiety",
        "Description": "Anxiety",
        "BlockElements": [
          { "Type": "Question", "QuestionID": "Q_Anxiety" }
        ]
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Anxiety",
      "Payload": {
        "QuestionID": "Q_Anxiety",
        "QuestionText": "Please rate the following statements.",
        "QuestionType": "Matrix",
        "Selector": "Likert",
        "Choices": {
          "1": {"Display": "I felt nervous during this task."},
          "2": {"Display": "I worried about selecting an incorrect article."},
          "3": {"Display": "I felt overwhelmed by the number of search results."}
        },
        "Answers": {
          "1": {"Display": "Strongly Disagree"},
          "2": {"Display": "Disagree"},
          "3": {"Display": "Neutral"},
          "4": {"Display": "Agree"},
          "5": {"Display": "Strongly Agree"}
        }
      }
    },

    /* -------------------- BLOCK: SUS -------------------- */
    {
      "Element": "BL",
      "PrimaryAttribute": "BL_SUS",
      "Payload": {
        "BlockID": "BL_SUS",
        "Description": "System Usability Scale",
        "BlockElements": [
          { "Type": "Question", "QuestionID": "Q_SUS" }
        ]
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_SUS",
      "Payload": {
        "QuestionID": "Q_SUS",
        "QuestionText": "Please rate the following statements.",
        "QuestionType": "Matrix",
        "Selector": "Likert",
        "Choices": {
          "1": {"Display": "I think I would like to use this system frequently."},
          "2": {"Display": "I found the system unnecessarily complex."},
          "3": {"Display": "I thought the system was easy to use."},
          "4": {"Display": "I think I would need assistance to use the system."},
          "5": {"Display": "I found the functions were well integrated."},
          "6": {"Display": "I thought the system had too much inconsistency."},
          "7": {"Display": "I imagine most people would learn this system quickly."},
          "8": {"Display": "I found the system cumbersome to use."},
          "9": {"Display": "I felt confident using the system."},
          "10": {"Display": "I needed to learn a lot before I could get going."}
        },
        "Answers": {
          "1": {"Display": "Strongly Disagree"},
          "2": {"Display": "Disagree"},
          "3": {"Display": "Neutral"},
          "4": {"Display": "Agree"},
          "5": {"Display": "Strongly Agree"}
        }
      }
    },

    /* -------------------- BLOCK: Comprehension -------------------- */
    {
      "Element": "BL",
      "PrimaryAttribute": "BL_Comprehension",
      "Payload": {
        "BlockID": "BL_Comprehension",
        "Description": "Comprehension",
        "BlockElements": [
          { "Type": "Question", "QuestionID": "Q_Explain" },
          { "Type": "Question", "QuestionID": "Q_Confidence" }
        ]
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Explain",
      "Payload": {
        "QuestionID": "Q_Explain",
        "QuestionText": "In 2–3 sentences, explain how the article addresses the research question.",
        "QuestionType": "TE",
        "Selector": "SL"
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Confidence",
      "Payload": {
        "QuestionID": "Q_Confidence",
        "QuestionText": "How confident are you that the selected article is relevant?",
        "QuestionType": "MC",
        "Selector": "SAVR",
        "Choices": {
          "1": {"Display": "Not at all confident"},
          "2": {"Display": "Slightly confident"},
          "3": {"Display": "Moderately confident"},
          "4": {"Display": "Very confident"},
          "5": {"Display": "Extremely confident"}
        }
      }
    },

    /* -------------------- BLOCK: AI Helpfulness -------------------- */
    {
      "Element": "BL",
      "PrimaryAttribute": "BL_AIHelp",
      "Payload": {
        "BlockID": "BL_AIHelp",
        "Description": "ChatGPT Helpfulness",
        "BlockElements": [
          { "Type": "Question", "QuestionID": "Q_AIHelp" }
        ]
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_AIHelp",
      "Payload": {
        "QuestionID": "Q_AIHelp",
        "QuestionText": "Rate ChatGPT’s usefulness during the task.",
        "QuestionType": "Matrix",
        "Selector": "Likert",
        "Choices": {
          "1": {"Display": "ChatGPT helped refine queries."},
          "2": {"Display": "ChatGPT helped interpret abstracts."},
          "3": {"Display": "ChatGPT helped evaluate article relevance."}
        },
        "Answers": {
          "1": {"Display": "Not at all helpful"},
          "2": {"Display": "Slightly helpful"},
          "3": {"Display": "Moderately helpful"},
          "4": {"Display": "Very helpful"},
          "5": {"Display": "Extremely helpful"}
        }
      }
    },

    /* -------------------- BLOCK: Reflection -------------------- */
    {
      "Element": "BL",
      "PrimaryAttribute": "BL_Reflection",
      "Payload": {
        "BlockID": "BL_Reflection",
        "Description": "Reflection",
        "BlockElements": [
          { "Type": "Question", "QuestionID": "Q_Reflect1" },
          { "Type": "Question", "QuestionID": "Q_Reflect2" },
          { "Type": "Question", "QuestionID": "Q_Reflect3" }
        ]
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Reflect1",
      "Payload": {
        "QuestionID": "Q_Reflect1",
        "QuestionText": "What was the most challenging part of this task?",
        "QuestionType": "TE"
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Reflect2",
      "Payload": {
        "QuestionID": "Q_Reflect2",
        "QuestionText": "Describe the strategy you used to select your article.",
        "QuestionType": "TE"
      }
    },
    {
      "Element": "SQ",
      "PrimaryAttribute": "Q_Reflect3",
      "Payload": {
        "QuestionID": "Q_Reflect3",
        "QuestionText": "If you used ChatGPT, describe one way it changed your usual search behavior.",
        "QuestionType": "TE"
      }
    }
  ]
}
