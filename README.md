# QnABot-slim

基于 [QnABot 7.1.0](https://github.com/aws-solutions/qnabot-on-aws/releases/tag/v7.1.0) 调整的 CloudFormation template，以实现最小 IAM。

## 最小 IAM Policy 配置


* AmazonLexFullAccess
* AWSLambda_FullAccess
* qnabot-firehose-policy

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Sid": "VisualEditor0",
              "Effect": "Allow",
              "Action": "firehose:ListDeliveryStreams",
              "Resource": "*"
          },
          {
              "Sid": "VisualEditor1",
              "Effect": "Allow",
              "Action": "firehose:*",
              "Resource": "arn:aws:firehose:*:217553593248:deliverystream/QnABot*"
          }
      ]
  }
  ```

* qnabot-s3-policy

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "s3:*",
                  "s3-object-lambda:*"
              ],
              "Resource": [
                  "arn:aws:s3:::qnabot*/*",
                  "arn:aws:s3:::qnabot*",
                  "arn:aws:s3:::solutions-ap-southeast-1/*",
                  "arn:aws:s3:::solutions-ap-southeast-1"
              ]
          }
      ]
  }
  ```

* qnabot-ai-policy

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "es:*"
              ],
              "Resource": "*"
          },
          {
              "Effect": "Allow",
              "Action": [
                  "kendra:Query",
                  "kendra:Retrieve"
              ],
              "Resource": [
                  "arn:aws:kendra:*:*:index/*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "bedrock:InvokeModel"
              ],
              "Resource": [
                  "arn:aws:bedrock:*:*:foundation-model/*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "bedrock:Retrieve",
                  "bedrock:RetrieveAndGenerate"
              ],
              "Resource": [
                  "arn:aws:bedrock:*:*:knowledge-base/*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "sagemaker:InvokeEndpoint"
              ],
              "Resource": "*"
          },
          {
              "Effect": "Allow",
              "Action": [
                  "translate:TranslateText",
                  "comprehend:DetectDominantLanguage",
                  "comprehend:DetectEntities",
                  "comprehend:DetectKeyPhrases",
                  "comprehend:DetectPiiEntities",
                  "comprehend:ContainsPiiEntities",
                  "comprehend:DetectSentiment",
                  "comprehend:DetectSyntax",
                  "comprehend:DescribeEntityRecognizer",
                  "comprehend:ListEntityRecognizers"
              ],
              "Resource": "*"
          }
      ]
  }
  ```

* qnabot-apigateway-policy 

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": "apigateway:*",
              "Resource": [
                  "arn:aws:apigateway:*::/restapis/*",
                  "arn:aws:apigateway:*::/restapis",
                  "arn:aws:apigateway:*::/deployments",
                  "arn:aws:apigateway:*::/stages",
                  "arn:aws:apigateway:*::/documentation/versions",
                  "arn:aws:apigateway:*::/accoun",
                  "arn:aws:apigateway:*::/account"
              ]
          }
      ]
  }
  ```
* qnabot-cf-policy 

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "cloudformation:CreateChangeSet",
                  "cloudformation:CreateStack",
                  "cloudformation:DeleteStack",
                  "cloudformation:DescribeChangeSet",
                  "cloudformation:DescribeStackEvents",
                  "cloudformation:DescribeStackResource",
                  "cloudformation:DescribeStacks",
                  "cloudformation:ExecuteChangeSet",
                  "cloudformation:GetStackPolicy",
                  "cloudformation:GetTemplate",
                  "cloudformation:GetTemplateSummary",
                  "cloudformation:ListStackResources",
                  "cloudformation:ListStacks",
                  "cloudformation:UpdateStack",
                  "cloudformation:ValidateTemplate"
              ],
              "Resource": [
                  "arn:aws:cloudformation:*:*:*"
              ]
          }
      ]
  }
  ```

* qnabot-github-cognito-policy 

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "cognito-idp:CreateUserPool",
                  "cognito-idp:DescribeUserPool",
                  "cognito-idp:UpdateUserPool",
                  "cognito-idp:DeleteUserPool",
                  "cognito-idp:CreateUserPoolClient",
                  "cognito-idp:DescribeUserPoolClient",
                  "cognito-idp:UpdateUserPoolClient",
                  "cognito-idp:DeleteUserPoolClient",
                  "cognito-idp:AdminInitiateAuth",
                  "cognito-idp:AdminUserGlobalSignOut",
                  "cognito-idp:ListUserPoolClients",
                  "cognito-idp:GetGroup",
                  "cognito-idp:CreateGroup",
                  "cognito-idp:DeleteGroup",
                  "cognito-idp:AdminGetUser",
                  "cognito-idp:AdminCreateUser",
                  "cognito-idp:AdminDeleteUser",
                  "cognito-idp:AdminListGroupsForUser",
                  "cognito-idp:AdminAddUserToGroup",
                  "cognito-idp:AdminRemoveUserFromGroup"
              ],
              "Resource": [
                  "arn:aws:cognito-idp:*:*:userpool/*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "cognito-identity:DescribeIdentityPool",
                  "cognito-identity:CreateIdentityPool",
                  "cognito-identity:DeleteIdentityPool",
                  "cognito-identity:UpdateIdentityPool",
                  "cognito-identity:GetIdentityPoolRoles",
                  "cognito-identity:SetIdentityPoolRoles"
              ],
              "Resource": [
                  "arn:aws:cognito-identity:*:*:identitypool/*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "iam:PassRole"
              ],
              "Resource": [
                  "arn:aws:iam::*:role/*"
              ],
              "Condition": {
                  "StringLike": {
                      "iam:PassedToService": [
                          "cognito-identity.amazonaws.com",
                          "lex.amazonaws.com",
                          "lexv2.amazonaws.com",
                          "channels.lex.amazonaws.com",
                          "channels.lexv2.amazonaws.com"
                      ]
                  }
              }
          }
      ]
  }
  ```

* qnabot-event-policy

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "servicecatalog:AssociateAttributeGroup",
                  "servicecatalog:AssociateResource",
                  "servicecatalog:CreateApplication",
                  "servicecatalog:CreateAttributeGroup",
                  "servicecatalog:DeleteApplication",
                  "servicecatalog:DeleteAttributeGroup",
                  "servicecatalog:DisassociateAttributeGroup",
                  "servicecatalog:DisassociateResource",
                  "servicecatalog:GetApplication",
                  "servicecatalog:GetAttributeGroup",
                  "servicecatalog:TagResource",
                  "servicecatalog:UpdateApplication",
                  "servicecatalog:UpdateAttributeGroup"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "logs:CreateLogGroup",
                  "logs:CreateLogStream",
                  "logs:DeleteLogGroup",
                  "logs:DeleteLogStream",
                  "logs:DeleteResourcePolicy",
                  "logs:DescribeLogGroups",
                  "logs:DescribeLogStreams",
                  "logs:DescribeResourcePolicies",
                  "logs:GetLogEvents",
                  "logs:PutLogEvents",
                  "logs:PutResourcePolicy"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "sns:CreateTopic",
                  "sns:DeleteTopic",
                  "sns:GetTopicAttributes",
                  "sns:ListTopics",
                  "sns:Publish",
                  "sns:SetTopicAttributes",
                  "sns:Subscribe",
                  "sns:Unsubscribe"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "ssm:DeleteParameter",
                  "ssm:GetParameter",
                  "ssm:GetParameters",
                  "ssm:PutParameter",
                  "ssm:StartSession"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "dynamodb:CreateGlobalTable",
                  "dynamodb:CreateTable",
                  "dynamodb:DeleteItem",
                  "dynamodb:DeleteTable",
                  "dynamodb:DescribeContinuousBackups",
                  "dynamodb:DescribeGlobalTable",
                  "dynamodb:DescribeTable",
                  "dynamodb:DescribeTimeToLive",
                  "dynamodb:GetItem",
                  "dynamodb:PutItem",
                  "dynamodb:Query",
                  "dynamodb:Scan",
                  "dynamodb:UpdateContinuousBackups",
                  "dynamodb:UpdateGlobalTable",
                  "dynamodb:UpdateTable",
                  "dynamodb:UpdateTimeToLive"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "events:DeleteRule",
                  "events:DescribeRule",
                  "events:DisableRule",
                  "events:EnableRule",
                  "events:ListTargetsByRule",
                  "events:ListRuleNamesByTarget",
                  "events:PutRule",
                  "events:PutTargets",
                  "events:RemoveTargets"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "firehose:CreateDeliveryStream",
                  "firehose:DeleteDeliveryStream",
                  "firehose:DescribeDeliveryStream"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "kms:CancelKeyDeletion",
                  "kms:CreateKey",
                  "kms:Delete*",
                  "kms:Describe*",
                  "kms:Disable*",
                  "kms:Decrypt",
                  "kms:Enable*",
                  "kms:EnableKey",
                  "kms:Encrypt",
                  "kms:GenerateDataKey",
                  "kms:Get*",
                  "kms:List*",
                  "kms:PutKeyPolicy",
                  "kms:Put*",
                  "kms:Revoke*",
                  "kms:ScheduleKeyDeletion",
                  "kms:UpdateKeyDescription",
                  "kms:Update*"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "cloudwatch:DeleteDashboards",
                  "cloudwatch:GetDashboard",
                  "cloudwatch:GetMetricStatistics",
                  "cloudwatch:ListDashboards",
                  "cloudwatch:PutDashboard"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "cloudfront:CreateCloudFrontOriginAccessIdentity",
                  "cloudfront:CreateDistribution",
                  "cloudfront:CreateResponseHeadersPolicy",
                  "cloudfront:DeleteCloudFrontOriginAccessIdentity",
                  "cloudfront:DeleteDistribution",
                  "cloudfront:DeleteResponseHeadersPolicy",
                  "cloudfront:GetCloudFrontOriginAccessIdentity",
                  "cloudfront:GetDistribution",
                  "cloudfront:GetResponseHeadersPolicy",
                  "cloudfront:TagResource",
                  "cloudfront:UnTagResource",
                  "cloudfront:UpdateCloudFrontOriginAccessIdentity",
                  "cloudfront:UpdateDistribution",
                  "cloudfront:UpdateResponseHeadersPolicy"
              ],
              "Resource": [
                  "*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "chatbot:*",
                  "codebuild:*",
                  "codecommit:*",
                  "codestar-connections:*",
                  "codestar-notifications:*",
                  "ec2:DescribeVpcs",
                  "ec2:DescribeSecurityGroups",
                  "ec2:DescribeSubnets",
                  "ecr:DescribeRepositories",
                  "ecr:ListImages",
                  "elasticfilesystem:DescribeFileSystems",
                  "s3:GetBucketLocation",
                  "s3:ListAllMyBuckets",
                  "sqs:CreateQueue",
                  "sqs:SendMessage",
                  "secretsmanager:CreateSecret",
                  "secretsmanager:UpdateSecret",
                  "secretsmanager:DeleteSecret"
              ],
              "Resource": "*"
          },
          {
              "Effect": "Allow",
              "Action": [
                  "wafv2:AssociateWebACL",
                  "wafv2:CreateWebACL",
                  "wafv2:DeleteWebACL",
                  "wafv2:UpdateWebACL"
              ],
              "Resource": [
                  "*"
              ]
          }
      ]
  }
  ```

* qnabot-iam-restrict-policy

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "iam:AttachRolePolicy",
                  "iam:CreatePolicy",
                  "iam:CreatePolicyVersion",
                  "iam:CreateRole",
                  "iam:CreateServiceLinkedRole",
                  "iam:DeletePolicy",
                  "iam:DeleteRole",
                  "iam:DeleteRolePolicy",
                  "iam:DeletePolicyVersion",
                  "iam:DeleteServiceLinkedRole",
                  "iam:DetachRolePolicy",
                  "iam:GetPolicy",
                  "iam:GetRole",
                  "iam:GetServiceLinkedRoleDeletionStatus",
                  "iam:ListPolicyVersions",
                  "iam:PutRolePolicy",
                  "iam:UpdateRole"
              ],
              "Resource": [
                  "arn:aws:iam::*:role/QnABot*",
                  "arn:aws:iam::*:role/aws-service-role/*",
                  "arn:aws:iam::*:role/stacksets-exec*",
                  "arn:aws:iam::*:policy/QnABot*"
              ]
          },
          {
              "Effect": "Allow",
              "Action": [
                  "iam:PassRole"
              ],
              "Resource": [
                  "arn:aws:iam::*:role/QnABot*",
                  "arn:aws:iam::*:role/aws-service-role/*",
                  "arn:aws:iam::*:role/stacksets-exec*"
              ],
              "Condition": {
                  "StringLike": {
                      "iam:PassedToService": [
                          "cognito-identity.amazonaws.com",
                          "lex.amazonaws.com",
                          "lexv2.amazonaws.com",
                          "channels.lex.amazonaws.com",
                          "channels.lexv2.amazonaws.com",
                          "cloudformation.amazonaws.com",
                          "opensearchservice.amazonaws.com",
                          "es.amazonaws.com",
                          "lambda.amazonaws.com",
                          "kendra.amazonaws.com",
                          "firehose.amazonaws.com",
                          "apigateway.amazonaws.com"
                      ]
                  }
              }
          }
      ]
  }
  ```