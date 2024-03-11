## moneysign-sdk

# MoneySign® Flutter SDK

> ### Overview: 
- MoneySign SDK is a Software Development Kit that will help developers integrate MoneySign Assessment into their app according to 1 Finance way.
- This SDK will contain the Assessment questions, Progress Measurement, MoneySign Generation, and MoneySign Result.
- It will also be used to sell it as a product in external apps by featuring MoneySign in their apps. 

> ### Key Features: 
- MoneySign end-to-end flow
- Store MoneySign for your users
- MoneySign progress
- MoneySign report

> ### Rules: 
- User Authentication is required with Customer ID only.
- MoneySign UI flow will be Non-customizable.

> ### Tech:
- Which UI component needs to be included?
- Are we integrating different APIs and Servers apart from 1F Prod?
- How do we need to authenticate users to start MoneySign?
- Do we need to expose callback APIs, if users leave the SDK flow?
- How to manage the Progress of assessment?

> # MS SDK APIs

### User Onboarding


1. Request OTP 
- [POST] `https://newdev.customer.onefin.app/api/v2/onboarding/request-for-otp`
> Request
```
{
  "mobile_number": "string"
}
```
> Response
```
{
  "status_code": 200,
  "error": "string",
  "message": "OTP Sent Successfully.",
  "data": {}
}
```

2. Validate OTP 
- [POST] `https://newdev.customer.onefin.app/api/v2/onboarding/validate-otp`
> Request
```
{
  "mobile_number": "string",
  "otp": "string",
  "customer_app_instance_id": "string"
}
```
> Response
```
{
  "status_code": 200,
  "error": "string",
  "message": "Success.",
  "data": {
    "otp_valid": false,
    "temp_code": "",
    "customer_found": false,
    "access_token": "",
    "user_id": "",
    "first_name": "",
    "last_name": "",
    "mobile_number": ""
  }
}
```

3. Onboard User 
- [POST] `https://newdev.customer.onefin.app/api/v2/onboarding/onboard-customer`
> Request
```
{
  "first_name": "string",
  "last_name": "string",
  "mobile_number": "string",
  "temp_code": "string",
  "customer_app_instance_id": "string"
}
```
> Response
```
{
  "status_code": 200,
  "error": "string",
  "message": "Success.",
  "data": {
    "access_token": "",
    "user_id": "",
    "first_name": "",
    "last_name": "",
    "mobile_number": ""
  }
}
```

-----------
### MoneySign


1. MS Stage API 
- [GET] `https://newdev.ms.onefin.app/api/user/moneysign/1/stage?ms_validate=false`
> Response [if false, then questions will be fetched] 
```
{
  "status": 200,
  "message": "SUCCESS",
  "error": "",
  "stackTrace": "",
  "data": {
    "moneySign": "",
    "moneysign_id": 0,
    "isMoneySignGenerated": false,
    "noOfQuestionsFilled": 0,
    "question_answered_per": 0,
    "total_questions": 25,
    "is_assesment_start": true,
    "msgenerated_time": null,
    "previous": null,
    "active": {
      "question_id": 1,
      "question": "How often I search for new investment options:",
      "instruction": null,
      "is_last_question": false,
      "is_first_question": true,
      "question_type": 1,
      "answers": [
        {
          "option": "Never",
          "score": "1",
          "answer_id": 85,
          "is_none": false,
          "sequence": 1,
          "is_selected": false
        },
        {
          "option": "Whenever I hear someone talking about it",
          "score": "2",
          "answer_id": 84,
          "is_none": false,
          "sequence": 2,
          "is_selected": false
        }
      ]
    }
  }
}
```


2. Add Response 
- [POST] `https://newdev.ms.onefin.app/api/user/money-sign/add-response`
> Request
```
{
  "is_last_question": false,
  "userCode": "273695-2744-3334-343444",
  "getuserDetails": {
    "firstName": "string",
    "lastName": "string",
    "mobileNumber": "1000000000"
  },
  "answers": [
    {
      "questionId": "1",
      "scores": [
        "1"
      ],
      "answerids": [
        "85"
      ]
    }
  ]
}
```
> Response
```
{
  "status": 200,
  "message": "SUCCESS",
  "error": "",
  "stackTrace": "",
  "data": {
    "isMoneySignGenerated": false,
    "moneySign": "",
    "noOfQuestionsFilled": 1,
    "noOfQuestionsFilledPer": 4,
    "lastAnswerId": [
      85
    ],
    "lastAnswerScore": [
      1
    ],
    "ms_data": {
      "moneySign": "",
      "moneysign_id": 0,
      "isMoneySignGenerated": false,
      "noOfQuestionsFilled": 1,
      "question_answered_per": 0,
      "total_questions": 25,
      "is_assesment_start": true,
      "msgenerated_time": null,
      "previous": {
        "question_id": 1,
        "question": "How often I search for new investment options:",
        "instruction": null,
        "is_last_question": false,
        "is_first_question": true,
        "question_type": 1,
        "answers": [
          {
            "option": "Never",
            "score": "1",
            "answer_id": 85,
            "is_none": false,
            "sequence": 1,
            "is_selected": true
          },
          {
            "option": "Whenever I hear someone talking about it",
            "score": "2",
            "answer_id": 84,
            "is_none": false,
            "sequence": 2,
            "is_selected": false
          },
          {
            "option": "Once a month",
            "score": "3",
            "answer_id": 83,
            "is_none": false,
            "sequence": 3,
            "is_selected": false
          },
          {
            "option": "2 – 3 times a week",
            "score": "4",
            "answer_id": 82,
            "is_none": false,
            "sequence": 4,
            "is_selected": false
          },
          {
            "option": "Daily",
            "score": "5",
            "answer_id": 81,
            "is_none": false,
            "sequence": 5,
            "is_selected": false
          }
        ]
      },
      "active": {
        "question_id": 24,
        "question": "Investment options that I’m aware of:",
        "instruction": "Select all options that apply",
        "is_last_question": false,
        "is_first_question": false,
        "question_type": 2,
        "answers": [
          {
            "option": "Gold Exchange-Traded Funds (ETFs)",
            "score": "0.25",
            "answer_id": 88,
            "is_none": false,
            "sequence": 1,
            "is_selected": false
          },
          {
            "option": "Real Estate Investment Trusts (REITs)",
            "score": "0.4277",
            "answer_id": 99,
            "is_none": false,
            "sequence": 2,
            "is_selected": false
          },
          {
            "option": "International / Overseas Funds",
            "score": "0.6918",
            "answer_id": 100,
            "is_none": false,
            "sequence": 3,
            "is_selected": false
          }
        ]
      }
    }
  }
}
```


3. Generate MoneySign 
- [POST] `https://newdev.ms.onefin.app/api/user/money-sign/generate`
> Response
```
{
  "status_code": 200,
  "error": "string",
  "message": "Success",
  "data": {}
}
```

4. MoneySign Details 
- [POST] `https://newdev.ms.onefin.app/api/user/money-sign/moneysigndetails`
> Request
```
```
> Response
```
```
