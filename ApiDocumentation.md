
> # MS SDK APIs

Postman Collection 
- https://elements.getpostman.com/redirect?entityId=18661171-17de362e-31c3-44ca-9f68-fbfe723070bf&entityType=collection

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
  status": 200,
  "message": "SUCCESS",
  "error": "",
  "stackTrace": "",
  "data": {
    "moneysign": "Far-sighted Eagle",
    "description": "You’re a committed individual who possesses...",
    "strength": [
      "Sharp focus",
      "Broad vision",
      "Boldness"
    ],
    "weakness": [
      "Sticking with bad decisions",
      "Hyperactivity",
      "Overconfidence"
    ]
  }
}
```

4. MoneySign Details 
- [POST] `https://newdev.ms.onefin.app/api/user/money-sign/moneysigndetails`
> Response
```
{
  "status": 200,
  "message": "SUCCESS",
  "error": "",
  "stackTrace": "",
  "data": {
    "moneysign": "Far-sighted Eagle",
    "description": "You’re a committed individual who possesses...",
    "isFeedbackSaved": false,
    "ms_doc": "https://automated-bakup-rds.s3.amazonaws.com/1629a63f-5c3f-41c2-a091-f8f5588141ac/moneysign.pdf",
    "strength": [
      "Sharp focus",
      "Broad vision",
      "Boldness"
    ],
    "weakness": [
      "Sticking with bad decisions",
      "Hyperactivity",
      "Overconfidence"
    ]
  }
}
```
