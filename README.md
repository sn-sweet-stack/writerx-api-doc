# Documentation Api

## API Endpoints

- [Authentication](#Authentication)
  - [Login](#Login)
- [Websites](#Websites)
  - [Add website](#Add-website)
  - [Get list websites](#Get-list-websites)
  - [Delete website](#Delete-website)
- [Api keys](#Api-keys)
  - [Add api keys](#Add-api-keys)
- [Profile](#Profile)
  - [Get profile](#Get-profile)
  - [Update profile](#Update-profile)
- [Ai](#Ai)
    - [Ai assistants](#Ai-assistants)
        - [Get list assistants](#Get-list-assistants)
        - [Add assistant](#Add-assistant)
        - [Delete assistant](#Delete-assistant)
        - [Update assistant](#Update-assistant)
        - [Get list assistants external](#Get-list-assistants-external)
    - [AI Service](#AI-Service)
        - [Get list services](#Get-list-services)
    - [AI Models](#AI-Models)
        - [Get list models](#Get-list-models)
    - [AI Brand](#AI-Brand)
        - [Get list brands](#Get-list-brands)
- [Generation Jobs](#Generation-Jobs)
  - [List jobs](#List-jobs)
  - [Create job](#Create-job)
  - [Create job settings](#Create-job-settings)
  - [Get job settings](#Get-job-settings)
  - [Get job setting data](#Get-job-setting-data)
  - [Delete job settings](#Delete-job-settings)
  - [Stop Job](#Stop-Job)
  - [Start Job](#Start-Job)
  - [Delete job](#Delete-job)
- [Dataset](#Dataset)
  - [List datasets](#List-datasets)
  - [Get Dataset Values](#Get-Dataset-Values)
- [Content](#Content)
  - [List content](#List-content)
  - [Delete content](#Delete-content)
  - [Stop Generation Content](#Stop-Generation-Content)
  - [Start Generation Content](#Start-Generation-Content)
  - [Get content](#Get-content)
  - [Update content](#Update-content)
  - [Regenerate Step content](#Regenerate-Step-content)
  - [Stop Generation Content](#Stop-Generation-Content)
  - [Start Generation Content](#Start-Generation-Content)
- [Publication Calendar](#Publication-Calendar)
  - [List publication calendar](#List-publication-calendar)
- [WordPress](#wordpress-data)
  - [Get authors](#get-authors)
  - [Get categories](#get-categories)
  - [Get tags](#get-tags)
  - [Get templates](#get-templates)
  - [Get post types](#get-post-types)


---
# Authentication

## Login

**URL:** `/api/auht/login`

**Method:** `POST`

**Describe:** This endpoint is used to authenticate a user. The user must provide a valid email and password.

**Success:**
- Code: `200 OK`
- Body response: 
```json
{
    "data": {
      "token": "token",
      "type": "Bearer"
    }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response: 
```json
{
  "message": "Email or password is incorrect"
}
```
---

# Websites

## Add website

**URL:** `/api/website/`

**Method:** `POST`

**Describe:** This endpoint is used to add a website to the database.

**Body request:**
```json
{
  "title": "string",
  "url": "string",
  "api_credentials": "string",
  "assistant_id": "string"
}
```

**Success:**
- Code: `200 OK`
- Body response:
```json
{
    "data": {
      "title": "string",
      "url": "string",
      "api_credential": "string",
      "assistant_id": "string"
    }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

**Error:**
- Code: `400 Bad Request`
- Body response:
```json
{
  "message": "api_credentials is invalid"
}
```
- Code: `422 Unprocessable Entity`
- Body response:
```json
{
  "message": "The given data was invalid.",
  "errors":{
    "title": ["The title field is required."],
    "url": ["The url field is required."],
    "api_credentials": ["The api credentials field is required."],
    "assistant_id": ["The assistant id field is required."]
  }
}
```

## Get list websites

**URL:** `/api/website/`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of websites from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "title": "string",
      "url": "string",
      "api_credential": "string",
      "assistant_id": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

## Delete website

**URL:** `/api/website/{id}`

**Method:** `DELETE`

**Describe:** This endpoint is used to delete a website from the database.

**Params:**
- `id` - website id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "title": "string",
      "url": "string",
      "api_credential": "string",
      "assistant_id": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to delete this website"
}
```
---

# Api keys

## Add api keys

**URL:** `/api/keys/{id}`

**Method:** `POST`

**Describe:** This endpoint is used to add api keys to the database.

**Body request:**
```json
[
  {
    "service": "string",
    "value": "string"
  }  
]
```

**Success:**
- Code: `200 OK`
- Body response:
```json
{
    "data": [
      {
        "service": "string",
        "value": "string"
      }
    ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

**Error:**
- Code: `422 Unprocessable Entity`
- Body response:
```json
{
  "message": "The given data was invalid.",
    "errors":{
        "*.service": ["The service field is required."],
        "*.value": ["The value field is required."]
    }
}
```

---


# Profile

## Get profile

**URL:** `/api/profile`

**Method:** `GET`

**Describe:** This endpoint is used to get the profile of the user.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "name": "string",
    "email": "string",
    "created_at": "string",
    "updated_at": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

## Update profile

**URL:** `/api/profile`

**Method:** `PUT`

**Describe:** This endpoint is used to update the profile of the user.

**Body request:**
```json
{
  "name": "string",
  "email": "string",
  "old_password": "string|nullable",
  "new_password": "string|nullable"
}
```

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "name": "string",
    "email": "string",
    "created_at": "string",
    "updated_at": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `422 Unprocessable Entity`
- Body response:
```json
{
  "message": "The given data was invalid.",
  "errors":{
    "name": ["The name field is required."],
    "email": ["The email field is required."],
    "old_password": ["The old password field is required."],
    "new_password": ["The new password field is required."]
  }
}
```
---

# Ai

## Ai assistants

### Get list assistants

**URL:** `/api/ai/assistants`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of assistants from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "name": "string",
      "service": {
        "id": "string",
        "name": "string"
      },
      "assistant_id": "string",
      "service_id": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

### Add assistant

**URL:** `/api/ai/assistants`

**Method:** `POST`

**Describe:** This endpoint is used to add an assistant to the database.

**Body request:**
```json
{
  "name": "string",
  "service_id": "string",
  "assistant_id": "string"
}
```

**Success:**
- Code: `201 Created`
- Body response:
```json
{
  "data": {
    "name": "string",
    "service": {
      "id": "string",
      "name": "string"
    },
    "assistant_id": "string",
    "service_id": "string",
    "created_at": "string",
    "updated_at": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `422 Unprocessable Entity`
- Body response:
```json
{
  "message": "The given data was invalid.",
  "errors":{
    "name": ["The name field is required."],
    "service_id": ["The service id field is required."],
    "assistant_id": ["The assistant id field is required."]
  }
}
```

### Delete assistant

**URL:** `/api/ai/assistants/{id}`

**Method:** `DELETE`

**Describe:** This endpoint is used to delete an assistant from the database.

**Params:**
- `id` - assistant id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "name": "string",
    "service": {
      "id": "string",
      "name": "string"
    },
    "assistant_id": "string",
    "service_id": "string",
    "created_at": "string",
    "updated_at": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to delete this assistant"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Assistant not found"
}
```

### Update assistant

**URL:** `/api/ai/assistants/{id}`

**Method:** `PUT`

**Describe:** This endpoint is used to update an assistant from the database.

**Params:**
- `id` - assistant id

**Body request:**
```json
{
  "name": "string",
  "service_id": "string",
  "assistant_id": "string"
}
```

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "name": "string",
    "service": {
      "id": "string",
      "name": "string"
    },
    "assistant_id": "string",
    "service_id": "string",
    "created_at": "string",
    "updated_at": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `422 Unprocessable Entity`
- Body response:
```json
{
  "message": "The given data was invalid.",
  "errors":{
    "name": ["The name field is required."],
    "service_id": ["The service id field is required."],
    "assistant_id": ["The assistant id field is required."]
  }
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Assistant not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to update this assistant"
}
```

### Get list assistants external

**URL:** `/api/ai/assistants/external`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of assistants from the external service.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "id": "string",
      "name": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Service not found"
}
```
---

## AI Service

### Get list services

**URL:** `/api/ai/services`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of services from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "name": "string",
      "id": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
---

## AI Models

### Get list models

**URL:** `/api/ai/models`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of models from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "name": "string",
      "id": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

## AI Brand

### Get list brands

**URL:** `/api/ai/brands`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of brands from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "name": "string",
      "id": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

# Generation Jobs

## List jobs

**URL:** `/api/jobs`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of jobs from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "id": "string",
      "status": "string",
      "name": "string",
      "articles_count": "int",
      "articles_done": "int",
      "started_at": "datetime",
      "completed_at": "datetime",
      "created_at": "datetime",
      "updated_at": "datetime"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

## Create job

**URL:** `/api/jobs`

**Method:** `POST`

**Describe:** This endpoint is used to create a job in the database.

**Body request:**
```json
{
  "topic": "string",
  "main_keyphrase": "string",
  "additional_keyphrase": "string",
  "sections": "int",
  "paragraphs": "int",
  "min_words": "int",
  "max_words": "int",
  "is_bulk": "bool",
  "website_id": "string",
  "variables": [
    {
      "name": "string",
      "dataset_id": "string"
    }
  ],
  "post_settings": {
    "post_type": "string",
    "use_template": "string",
    "assistant_author": "string"
  },
  "content_settings": {
    "prompt_title": "string",
    "prompt_excerpt": "string",
    "prompt_meta_keywords": "string",
    "prompt_meta_description": "string",
    "generate_meta_keywords": "bool",
    "generate_meta_description": "bool",
    "generate_excerpt": "bool"
  },
  "image_settings": {
    "use_image": "bool"
  },
  "seo_settings": {
    "use_seo": "bool"
  },
  "category_settings": {
    "use_category": "bool",
    "count_category": "int",
    "use_tags": "bool",
    "count_tags": "int",
    "categories": [
      "string"
    ],
    "tags": [
      "string"
    ]
  },
  "publish_settings": {
    "publish_type": "string",
    "publish_date": "datetime"
  },
  "write_settings": {
    "write_tone": "string",
    "write_style": "string"
  },
  "ai_settings": {
    "assistant_id": "string",
    "brand_id": "string",
    "model_id": "string",
    "temperature": "double",
    "max_tokens": "int"
  },
  "generate_method": "string"
}
```

**Success:**
- Code: `201 Created`
- Body response:
```json
{
  "data": {
    "id": "string",
    "status": "string",
    "name": "string",
    "articles_count": "int",
    "articles_done": "int",
    "started_at": "datetime",
    "completed_at": "datetime",
    "created_at": "datetime",
    "updated_at": "datetime"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `422 Unprocessable Entity`
- Body response:
```json
{
  "message": "The given data was invalid.",
  "errors":{
    "topic": ["The topic field is required."],
    "main_keyphrase": ["The main keyphrase field is required."],
    "additional_keyphrase": ["The additional keyphrase field is required."],
    "sections": ["The sections field is required."],
    "paragraphs": ["The paragraphs field is required."],
    "min_words": ["The min words field is required."],
    "max_words": ["The max words field is required."],
    "is_bulk": ["The is bulk field is required."],
    "variables": ["The variables field is required."],
    "post_settings": ["The post settings field is required."],
    "content_settings": ["The content settings field is required."],
    "image_settings": ["The image settings field is required."],
    "seo_settings": ["The seo settings field is required."],
    "category_settings": ["The category settings field is required."],
    "publish_settings": ["The publish settings field is required."],
    "write_settings": ["The write settings field is required."],
    "ai_settings": ["The ai settings field is required."],
    "generate_method": ["The generate method field is required."]
  }
}
```

## Create job settings

**URL:** `/api/jobs/settings`

**Method:** `POST`

**Describe:** This endpoint is used to create a job settings in the database.

**Body request:** 
```json
{
  "name_save": "string",
  "topic": "string",
  "main_keyphrase": "string",
  "additional_keyphrase": "string",
  "sections": "int",
  "paragraphs": "int",
  "min_words": "int",
  "max_words": "int",
  "is_bulk": "bool",
  "website_id": "string",
  "variables": [
    {
      "name": "string",
      "dataset_id": "string"
    }
  ],
  "post_settings": {
    "post_type": "string",
    "use_template": "string",
    "assistant_author": "string"
  },
  "content_settings": {
    "prompt_title": "string",
    "prompt_excerpt": "string",
    "prompt_meta_keywords": "string",
    "prompt_meta_description": "string",
    "generate_meta_keywords": "bool",
    "generate_meta_description": "bool",
    "generate_excerpt": "bool"
  },
  "image_settings": {
    "use_image": "bool"
  },
  "seo_settings": {
    "use_seo": "bool"
  },
  "category_settings": {
    "use_category": "bool",
    "count_category": "int",
    "use_tags": "bool",
    "count_tags": "int",
    "categories": [
      "string"
    ],
    "tags": [
      "string"
    ]
  },
  "publish_settings": {
    "publish_type": "string",
    "publish_date": "datetime"
  },
  "write_settings": {
    "write_tone": "string",
    "write_style": "string"
  },
  "ai_settings": {
    "assistant_id": "string",
    "brand_id": "string",
    "model_id": "string",
    "temperature": "double",
    "max_tokens": "int"
  },
  "generate_method": "string"
}
```

## Get job settings

**URL:** `/api/jobs/settings`

**Method:** `GET`

**Describe:** This endpoint is used to get a job settings from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "name_save": "string",
    "id": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

## Get job setting data

**URL:** `/api/jobs/settings/{id}`

**Method:** `GET`

**Describe:** This endpoint is used to get a job setting data from the database.

**Params:**
- `id` - job setting id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "name_save": "string",
    "topic": "string",
    "main_keyphrase": "string",
    "additional_keyphrase": "string",
    "sections": "int",
    "paragraphs": "int",
    "min_words": "int",
    "max_words": "int",
    "is_bulk": "bool",
    "website_id": "string",
    "variables": [
      {
        "name": "string",
        "dataset_id": "string"
      }
    ],
    "post_settings": {
      "post_type": "string",
      "use_template": "string",
      "assistant_author": "string"
    },
    "content_settings": {
      "prompt_title": "string",
      "prompt_excerpt": "string",
      "prompt_meta_keywords": "string",
      "prompt_meta_description": "string",
      "generate_meta_keywords": "bool",
      "generate_meta_description": "bool",
      "generate_excerpt": "bool"
    },
    "image_settings": {
      "use_image": "bool"
    },
    "seo_settings": {
      "use_seo": "bool"
    },
    "category_settings": {
      "use_category": "bool",
      "count_category": "int",
      "use_tags": "bool",
      "count_tags": "int",
      "categories": [
        "string"
      ],
      "tags": [
        "string"
      ]
    },
    "publish_settings": {
      "publish_type": "string",
      "publish_date": "datetime"
    },
    "write_settings": {
      "write_tone": "string",
      "write_style": "string"
    },
    "ai_settings": {
      "assistant_id": "string",
      "brand_id": "string",
      "model_id": "string",
      "temperature": "double",
      "max_tokens": "int"
    },
    "generate_method": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Job setting not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to get this job setting"
}
```

## Delete job settings

**URL:** `/api/jobs/settings/{id}`

**Method:** `DELETE`

**Describe:** This endpoint is used to delete a job settings from the database.

**Params:**
- `id` - job setting id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "name_save": "string",
    "id": "string"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to delete this job setting"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Job setting not found"
}
```

## Stop Job

**URL:** `/api/jobs/{id}/stop`

**Method:** `POST`

**Describe:** This endpoint is used to stop a job in the database.

**Params:**
- `id` - job id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "id": "string",
    "status": "string",
    "name": "string",
    "articles_count": "int",
    "articles_done": "int",
    "started_at": "datetime",
    "completed_at": "datetime",
    "created_at": "datetime",
    "updated_at": "datetime"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Job not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to stop this job"
}
```

## Start Job

**URL:** `/api/jobs/{id}/start`

**Method:** `POST`

**Describe:** This endpoint is used to start a job in the database.

**Params:**
- `id` - job id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "id": "string",
    "status": "string",
    "name": "string",
    "articles_count": "int",
    "articles_done": "int",
    "started_at": "datetime",
    "completed_at": "datetime",
    "created_at": "datetime",
    "updated_at": "datetime"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Job not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to start this job"
}
```

## Delete job

**URL:** `/api/jobs/{id}`

**Method:** `DELETE`

**Describe:** This endpoint is used to delete a job from the database.

**Params:**
- `id` - job id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "id": "string",
    "status": "string",
    "name": "string",
    "articles_count": "int",
    "articles_done": "int",
    "started_at": "datetime",
    "completed_at": "datetime",
    "created_at": "datetime",
    "updated_at": "datetime"
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to delete this job"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Job not found"
}
```

---

# Dataset

## List datasets

**URL:** `/api/datasets`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of datasets from the database.

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "name": "string",
      "id": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

## Get Dataset Values

**URL:** `/api/datasets/{id}/values`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of values from the dataset.

**Params:**
- `id` - dataset id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "value": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Dataset not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to get this dataset"
}
```

---

# Content

## List content

**URL:** `/api/content`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of content from the database.

**Query params:**
- `generate_id` - generate id
- `status` - status
- `website_id` - website id
- `published_start` - published start
- `published_end` - published end

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "title": "string",
      "status": "string",
      "url": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```

## Delete content

**URL:** `/api/content/{id}`

**Method:** `DELETE`

**Describe:** This endpoint is used to delete a content from the database.

**Params:**
- `id` - content id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "title": "string",
      "status": "string",
      "url": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to delete this content"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```

## Stop Generation Content

**URL:** `/api/content/{id}/stop`

**Method:** `POST`

**Describe:** This endpoint is used to stop a generation content from the database.

**Params:**
- `id` - content id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "title": "string",
      "status": "string",
      "url": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to stop this content"
}
```

## Start Generation Content

**URL:** `/api/content/{id}/start`

**Method:** `POST`

**Describe:** This endpoint is used to start a generation content from the database.

**Params:**
- `id` - content id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "title": "string",
      "status": "string",
      "url": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to start this content"
}
```

## Get content

**URL:** `/api/content/{id}`

**Method:** `GET`

**Describe:** This endpoint is used to get a content from the database.

**Params:**
- `id` - content id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "section": {
      "sections": "string",
      "is_done": "bool"
    },
    "content": {
      "post_content": "string",
      "is_done": "bool"
    },
    "meta_tags": {
      "title": "string",
      "meta_keywords": "string",
      "meta_description": "string",
      "is_done": "bool"
    },
    "post": {
      "post_type": "string",
      "author": "string",
      "template": "string",
      "is_done": "bool"
    },
    "category": {
      "category": [
        "string"
      ],
      "tags": [
        "string"
      ],
      "is_done": "bool"
    },
    "image": {
      "image_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "video": {
      "video_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "seo": {
      "todo": "string",
      "is_done": "bool"
    },
    "plagiarism": {
      "todo": "string",
      "is_done": "bool"
    },
    "publication": {
      "publication_date": "datetime",
      "post_facebook": "bool",
      "post_twitter": "bool",
      "post_linkedin": "bool"
    }
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to get this content"
}
```

## Update content

**URL:** `/api/content/{id}`

**Method:** `PUT`

**Describe:** This endpoint is used to update a content from the database.

**Params:**
- `id` - content id

**Body request:**
```json
{
  "section": {
    "sections": "string",
    "is_done": "bool"
  },
  "content": {
    "post_content": "string",
    "is_done": "bool"
  },
  "meta_tags": {
    "title": "string",
    "meta_keywords": "string",
    "meta_description": "string",
    "is_done": "bool"
  },
  "post": {
    "post_type": "string",
    "author": "string",
    "template": "string",
    "is_done": "bool"
  },
  "category": {
    "category": [
      "string"
    ],
    "tags": [
      "string"
    ],
    "is_done": "bool"
  },
  "image": {
    "image_url": [
      "string"
    ],
    "is_done": "bool"
  },
  "video": {
    "video_url": [
      "string"
    ],
    "is_done": "bool"
  },
  "seo": {
    "todo": "string",
    "is_done": "bool"
  },
  "plagiarism": {
    "todo": "string",
    "is_done": "bool"
  },
  "publication": {
    "publication_date": "datetime",
    "post_facebook": "bool",
    "post_twitter": "bool",
    "post_linkedin": "bool"
  }
}
```

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "section": {
      "sections": "string",
      "is_done": "bool"
    },
    "content": {
      "post_content": "string",
      "is_done": "bool"
    },
    "meta_tags": {
      "title": "string",
      "meta_keywords": "string",
      "meta_description": "string",
      "is_done": "bool"
    },
    "post": {
      "post_type": "string",
      "author": "string",
      "template": "string",
      "is_done": "bool"
    },
    "category": {
      "category": [
        "string"
      ],
      "tags": [
        "string"
      ],
      "is_done": "bool"
    },
    "image": {
      "image_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "video": {
      "video_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "seo": {
      "todo": "string",
      "is_done": "bool"
    },
    "plagiarism": {
      "todo": "string",
      "is_done": "bool"
    },
    "publication": {
      "publication_date": "datetime",
      "post_facebook": "bool",
      "post_twitter": "bool",
      "post_linkedin": "bool"
    }
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `422 Unprocessable Entity`
- Body response:
```json
{
  "message": "The given data was invalid.",
  "errors":{
    "section": ["The section field is required."],
    "content": ["The content field is required."],
    "meta_tags": ["The meta tags field is required."],
    "post": ["The post field is required."],
    "category": ["The category field is required."],
    "image": ["The image field is required."],
    "video": ["The video field is required."],
    "seo": ["The seo field is required."],
    "plagiarism": ["The plagiarism field is required."],
    "publication": ["The publication field is required."]
  }
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to update this content"
}
```

## Regenerate Step content

**URL:** `/api/content/{id}/regenerate-step/{step}`

**Method:** `POST`

**Describe:** This endpoint is used to regenerate a step content from the database.

**Params:**
- `id` - content id
- `step` - step [section, content, meta_tags, post, category, image, video, seo, plagiarism, publication]

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "section": {
      "sections": "string",
      "is_done": "bool"
    },
    "content": {
      "post_content": "string",
      "is_done": "bool"
    },
    "meta_tags": {
      "title": "string",
      "meta_keywords": "string",
      "meta_description": "string",
      "is_done": "bool"
    },
    "post": {
      "post_type": "string",
      "author": "string",
      "template": "string",
      "is_done": "bool"
    },
    "category": {
      "category": [
        "string"
      ],
      "tags": [
        "string"
      ],
      "is_done": "bool"
    },
    "image": {
      "image_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "video": {
      "video_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "seo": {
      "todo": "string",
      "is_done": "bool"
    },
    "plagiarism": {
      "todo": "string",
      "is_done": "bool"
    },
    "publication": {
      "publication_date": "datetime",
      "post_facebook": "bool",
      "post_twitter": "bool",
      "post_linkedin": "bool"
    }
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to regenerate this content"
}
```

## Stop step content

**URL:** `/api/content/{id}/stop-step/{step}`

**Method:** `POST`

**Describe:** This endpoint is used to stop a step content from the database.

**Params:**
- `id` - content id
- `step` - step [section, content, meta_tags, post, category, image, video, seo, plagiarism, publication]

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "section": {
      "sections": "string",
      "is_done": "bool"
    },
    "content": {
      "post_content": "string",
      "is_done": "bool"
    },
    "meta_tags": {
      "title": "string",
      "meta_keywords": "string",
      "meta_description": "string",
      "is_done": "bool"
    },
    "post": {
      "post_type": "string",
      "author": "string",
      "template": "string",
      "is_done": "bool"
    },
    "category": {
      "category": [
        "string"
      ],
      "tags": [
        "string"
      ],
      "is_done": "bool"
    },
    "image": {
      "image_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "video": {
      "video_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "seo": {
      "todo": "string",
      "is_done": "bool"
    },
    "plagiarism": {
      "todo": "string",
      "is_done": "bool"
    },
    "publication": {
      "publication_date": "datetime",
      "post_facebook": "bool",
      "post_twitter": "bool",
      "post_linkedin": "bool"
    }
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to stop this content"
}
```

## Start step content

**URL:** `/api/content/{id}/start-step/{step}`

**Method:** `POST`

**Describe:** This endpoint is used to start a step content from the database.

**Params:**
- `id` - content id
- `step` - step [section, content, meta_tags, post, category, image, video, seo, plagiarism, publication]

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": {
    "section": {
      "sections": "string",
      "is_done": "bool"
    },
    "content": {
      "post_content": "string",
      "is_done": "bool"
    },
    "meta_tags": {
      "title": "string",
      "meta_keywords": "string",
      "meta_description": "string",
      "is_done": "bool"
    },
    "post": {
      "post_type": "string",
      "author": "string",
      "template": "string",
      "is_done": "bool"
    },
    "category": {
      "category": [
        "string"
      ],
      "tags": [
        "string"
      ],
      "is_done": "bool"
    },
    "image": {
      "image_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "video": {
      "video_url": [
        "string"
      ],
      "is_done": "bool"
    },
    "seo": {
      "todo": "string",
      "is_done": "bool"
    },
    "plagiarism": {
      "todo": "string",
      "is_done": "bool"
    },
    "publication": {
      "publication_date": "datetime",
      "post_facebook": "bool",
      "post_twitter": "bool",
      "post_linkedin": "bool"
    }
  }
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code: `404 Not Found`
- Body response:
```json
{
  "message": "Content not found"
}
```
- Code: `403 Forbidden`
- Body response:
```json
{
  "message": "You don't have permission to start this content"
}
```

---

# Publication Calendar

## List publication calendar

**URL:** `/api/publication-calendar`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of publication calendar from the database.

**Query params:**
- `website_id` - website id
- `generate_id` - generate job id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "title": "string",
      "status": "string",
      "url": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

---

# WordPress Data

## Get authors

**URL:** `/api/wordpress/{site_id}/authors`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of authors from the WordPress.

**Params:**
- `site_id` - site id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "email": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code `404 Not Found`
- Body response:
```json
{
  "message": "Site not found"
}
```

## Get categories

**URL:** `/api/wordpress/{site_id}/categories`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of categories from the WordPress.

**Params:**
- `site_id` - site id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

## Get tags

**URL:** `/api/wordpress/{site_id}/tags`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of tags from the WordPress.

**Params:**
- `site_id` - site id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code `404 Not Found`
- Body response:
```json
{
  "message": "Site not found"
}
```

## Get templates

**URL:** `/api/wordpress/{site_id}/templates`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of templates from the WordPress.

**Params:**

- `site_id` - site id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code `404 Not Found`
- Body response:
```json
{
  "message": "Site not found"
}
```

## Get post types

**URL:** `/api/wordpress/{site_id}/post-types`

**Method:** `GET`

**Describe:** This endpoint is used to get a list of post types from the WordPress.

**Params:**
- `site_id` - site id

**Success:**
- Code: `200 OK`
- Body response:
```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "created_at": "string",
      "updated_at": "string"
    }
  ]
}
```

**Error:**
- Code: `401 Unauthorized`
- Body response:
```json
{
  "message": "Unauthorized"
}
```
- Code `404 Not Found`
- Body response:
```json
{
  "message": "Site not found"
}
```

---

[Go to top](#Documentation-Api)
