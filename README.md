# SDET Coding Exercise

## Avero Public API
Your task is to write automated tests against the Avero Public API. The API is specified via an [OpenAPI spec](./public_api_sdet_exercise.yaml) or see [the inline spec below](#avero-public-api-specification). You should run the API locally to test against. See [Running the API Locally](#running-the-api-locally) below for more information.

## Business Requirements
* Given the OpenAPI specification, write a test suite that evaluates the correctness of the following API endpoints:
    * `/v1/core/businesses`
    * `/v1/core/businesses/{businessIds}`
    * `/v1/sales/summary-sales`

## Expectations
* Tests can be written in any language or framework, so long as we can run them with minimal setup
* This exercise should take no more than 2-4 hours

## Delivery
* Your final output should be a link to a publicly hosted repo (e.g. GitHub, bitbucket) which includes all of your code, assets, etc. Anything that we need to run your project and wish us to evaluate.
* Your deliverable should include a README file with clear instructions for running your solution. 
    * Any dependencies, build commands, etc - every step after git clone … should be clearly documented.
    * **If we can’t run it, we can’t evaluate it!**
* If you wish to include any other resources (design docs, planning breakdown, etc), you may reference and link them from the README.
* When you're ready for us to review, you should email whoever you have been in contact with at Avero, providing:
    * A link to your publicly hosted repository
    * A rough estimate of how much time you spent (this isn't used in your evaluation but it does help us make sure we sized this exercise appropriately)
    * A short description of what your next steps would be if you had more time to work on this project

## Evaluation Criteria
1. We can run your tests
1. We can see the output of your tests
1. Your test suite is documented
1. Bugs in our API or your test suite are documented
    * For example, you found a bug in the API (congrats!). You have a test that fails with an explanation of why it fails.

---
## Running the API Locally
A mock version of the Avero Public API can be executed in a Docker container. It is this container against which you should write tests.

### Prerequisites
You will need the latest `stable` docker release. See the [Docker install instructions](https://docs.docker.com/install/) for more information.

### Steps to run

1. Pull the Docker image: `docker pull avero/sdet-coding-exercise`
2. Run the Docker image, opening up port 9000: `docker run -p 9000:9000 avero/sdet-coding-exercise`
3. You're all set. You can hit [http://localhost:9000/v1/core/businesses](http://localhost:9000/v1/core/businesses) in a browser and sanity check you get a response back

## Avero Public API Specification

```YAML
openapi: '3.0.2'

info:
  version: 1.0.0
  title: Avero Public API for SDET Exercise

servers:
  - url: http://localhost:9000
    description: Dockerized Public API

paths:
  /v1/core/businesses:
    get:
      summary: Retrieve the full list of the businesses (parents) and revenue centers (children) to which an account is entitled
      description: This resource describes the relationship between all businesses and revenue centers to which an API account is entitled.  The endpoint returns the hierarchy of businesses and revenue centers including IDs and names.
      operationId: getBusinesses
      responses:
        200:
          description: The hierarchy of businesses and revenue centers including IDs and names
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/BusinessResponse'
              example:
                data:
                  - businessId: '7047'
                    businessName: Blue Cafe
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123786'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123787'
                        revenueCenterName: Dining Room
                      - revenueCenterId: '5123820'
                        revenueCenterName: Banquet
                  - businessId: '6925'
                    businessName: Slingshot Cantina
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '4883762'
                        revenueCenterName: Bar
                      - revenueCenterId: '4883763'
                        revenueCenterName: Dining Room
                  - businessId: '7048'
                    businessName: Havana House
                    currencyCode: CAD
                    revenueCenters:
                      - revenueCenterId: '5123775'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123776'
                        revenueCenterName: Dining Room
                      - revenueCenterId: '5123800'
                        revenueCenterName: Banquet
                  - businessId: '7049'
                    businessName: Lotus
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123780'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123781'
                        revenueCenterName: Dining Room
                  - businessId: '7050'
                    businessName: Lotus NYC
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123889'
                        revenueCenterName: Banquet
                      - revenueCenterId: '5123890'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123891'
                        revenueCenterName: Dining Room
                  - businessId: '7051'
                    businessName: Sunflower Bar
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123883'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123884'
                        revenueCenterName: Dining Room
                  - businessId: '7052'
                    businessName: Sushi House
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123877'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123878'
                        revenueCenterName: Dining Room
                      - revenueCenterId: '5123880'
                        revenueCenterName: Banquet
                  - businessId: '7053'
                    businessName: The Chop Stick
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123974'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123975'
                        revenueCenterName: Dining Room
                  - businessId: '7054'
                    businessName: The Diner
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123980'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123981'
                        revenueCenterName: Dining Room
                      - revenueCenterId: '5124011'
                        revenueCenterName: Banquet
                  - businessId: '7055'
                    businessName: Village Inn
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5124052'
                        revenueCenterName: Bar
                      - revenueCenterId: '5124053'
                        revenueCenterName: Dining Room
                  - businessId: '10006'
                    businessName: Spark Nightclub & Lounge
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '10639802'
                        revenueCenterName: Banquet
                      - revenueCenterId: '10639803'
                        revenueCenterName: Dining Room
                      - revenueCenterId: '10639804'
                        revenueCenterName: Lounge
                      - revenueCenterId: '10639805'
                        revenueCenterName: Nightclub
                      - revenueCenterId: '10639820'
                        revenueCenterName: Private Dining
                meta: {}

  /v1/core/businesses/{businessIds}:
    get:
      summary: Retrieve businesses (parents) and revenue centers (children) under a specific business or businesses
      description: This resource describes the relationship between businesses and revenue centers for a specific business or businesses.  The endpoint returns the hierarchy of businesses and revenue centers including IDs and names.
      operationId: getBusinessesByIds
      parameters:
        - name: businessIds
          in: path
          description: A business ID or multiple business IDs.  Multiple business IDs must be comma separated.
          required: true
          schema:
            type: array
            items:
              type: string
            minItems: 1
            maxItems: 100
          style: simple
          example: 7047,6925
      responses:
        200:
          description: The hierarchy of businesses and revenue centers including IDs and names
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/BusinessResponse'
              example:
                data:
                  - businessId: '7047'
                    businessName: Blue Cafe
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '5123786'
                        revenueCenterName: Bar
                      - revenueCenterId: '5123787'
                        revenueCenterName: Dining Room
                      - revenueCenterId: '5123820'
                        revenueCenterName: Banquet
                  - businessId: '6925'
                    businessName: Slingshot Cantina
                    currencyCode: USD
                    revenueCenters:
                      - revenueCenterId: '4883762'
                        revenueCenterName: Bar
                      - revenueCenterId: '4883763'
                        revenueCenterName: Dining Room
                meta: {}

  /v1/sales/summary-sales:
    get:
      summary: Returns summary sales for businesses and business days.
      description: Returns summary sales data for all revenue centers under the parent business(es) requested.
        The response defaults to yesterday's business day if businessDays query parameter is not provided.
        The response defaults to all businesses that the account has access to if businessIds query parameter is not provided.
      operationId: getSummarySales
      parameters:
        - $ref: '#/components/parameters/optionalBusinessIds'
        - $ref: '#/components/parameters/optionalBusinessDays'
        - $ref: '#/components/parameters/optionalSalesAspectsToInclude'
      responses:
        200:
          description: A list of summary sales data
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/SummarySalesResponse'
              examples:
                noAspects:
                  summary: Summary sales businessIds=7047,6925&businessDays=2019-05-29
                  value:
                    data:
                      - organization:
                          name: Bar
                          level: revenueCenter
                          id: '4883762'
                          parent:
                            name: Slingshot Cantina
                            level: business
                            id: '6925'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '4207.75'
                          netSales: '4085.20'
                          coverCount: 5
                          checkCount: 137
                      - organization:
                          name: Dining Room
                          level: revenueCenter
                          id: '4883763'
                          parent:
                            name: Slingshot Cantina
                            level: business
                            id: '6925'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '12870.30'
                          netSales: '12544.00'
                          coverCount: 488
                          checkCount: 231
                      - organization:
                          name: Bar
                          level: revenueCenter
                          id: '5123786'
                          parent:
                            name: Blue Cafe
                            level: business
                            id: '7047'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '3683.55'
                          netSales: '3610.55'
                          coverCount: 2
                          checkCount: 107
                      - organization:
                          name: Dining Room
                          level: revenueCenter
                          id: '5123787'
                          parent:
                            name: Blue Cafe
                            level: business
                            id: '7047'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '17919.20'
                          netSales: '17423.65'
                          coverCount: 474
                          checkCount: 254
                      - organization:
                          name: Banquet
                          level: revenueCenter
                          id: '5123820'
                          parent:
                            name: Blue Cafe
                            level: business
                            id: '7047'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '960.40'
                          netSales: '960.40'
                          coverCount: 13
                          checkCount: 2
                    meta: {}
                withAspects:
                  summary: Summary sales businessIds=7047,6925&businessDays=2019-05-29&include=aspects.mealPeriods
                  value:
                    data:
                      - organization:
                          name: Bar
                          level: revenueCenter
                          id: '4883762'
                          parent:
                            name: Slingshot Cantina
                            level: business
                            id: '6925'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '4207.75'
                          netSales: '4085.20'
                          coverCount: 5
                          checkCount: 137
                        aspects:
                          mealPeriods:
                            - name: Dinner
                              metrics:
                                grossSales: '3195.00'
                                netSales: '3097.55'
                                coverCount: 2
                                checkCount: 95
                            - name: Late Night
                              metrics:
                                grossSales: '348.00'
                                netSales: '348.00'
                                coverCount: 3
                                checkCount: 17
                            - name: Lunch
                              metrics:
                                grossSales: '664.75'
                                netSales: '639.65'
                                coverCount: 0
                                checkCount: 25
                      - organization:
                          name: Dining Room
                          level: revenueCenter
                          id: '4883763'
                          parent:
                            name: Slingshot Cantina
                            level: business
                            id: '6925'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '12870.30'
                          netSales: '12544.00'
                          coverCount: 488
                          checkCount: 231
                        aspects:
                          mealPeriods:
                            - name: Dinner
                              metrics:
                                grossSales: '9448.50'
                                netSales: '9218.80'
                                coverCount: 322
                                checkCount: 152
                            - name: Late Night
                              metrics:
                                grossSales: '784.00'
                                netSales: '731.40'
                                coverCount: 33
                                checkCount: 19
                            - name: Lunch
                              metrics:
                                grossSales: '2637.80'
                                netSales: '2593.80'
                                coverCount: 133
                                checkCount: 60
                      - organization:
                          name: Bar
                          level: revenueCenter
                          id: '5123786'
                          parent:
                            name: Blue Cafe
                            level: business
                            id: '7047'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '3683.55'
                          netSales: '3610.55'
                          coverCount: 2
                          checkCount: 107
                        aspects:
                          mealPeriods:
                            - name: Dinner
                              metrics:
                                grossSales: '2706.25'
                                netSales: '2706.25'
                                coverCount: 2
                                checkCount: 77
                            - name: Late Night
                              metrics:
                                grossSales: '277.82'
                                netSales: '239.82'
                                coverCount: 0
                                checkCount: 10
                            - name: Lunch
                              metrics:
                                grossSales: '699.48'
                                netSales: '664.48'
                                coverCount: 0
                                checkCount: 20
                      - organization:
                          name: Dining Room
                          level: revenueCenter
                          id: '5123787'
                          parent:
                            name: Blue Cafe
                            level: business
                            id: '7047'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '17919.20'
                          netSales: '17423.65'
                          coverCount: 474
                          checkCount: 254
                        aspects:
                          mealPeriods:
                            - name: Breakfast
                              metrics:
                                grossSales: '912.00'
                                netSales: '878.50'
                                coverCount: 55
                                checkCount: 31
                            - name: Dinner
                              metrics:
                                grossSales: '10935.00'
                                netSales: '10797.00'
                                coverCount: 202
                                checkCount: 109
                            - name: Late Night
                              metrics:
                                grossSales: '368.25'
                                netSales: '368.25'
                                coverCount: 5
                                checkCount: 3
                            - name: Lunch
                              metrics:
                                grossSales: '5703.95'
                                netSales: '5379.90'
                                coverCount: 212
                                checkCount: 111
                      - organization:
                          name: Banquet
                          level: revenueCenter
                          id: '5123820'
                          parent:
                            name: Blue Cafe
                            level: business
                            id: '7047'
                        businessDay: '2019-05-29'
                        currencyCode: USD
                        metrics:
                          grossSales: '960.40'
                          netSales: '960.40'
                          coverCount: 13
                          checkCount: 2
                        aspects:
                          mealPeriods:
                            - name: Dinner
                              metrics:
                                grossSales: '960.40'
                                netSales: '960.40'
                                coverCount: 13
                                checkCount: 2
                    meta: {}

components:
  schemas:

    RevenueCenter:
      description: A revenue center is the lowest level of the organization and the owner of transactions.
        A revenue center is a child entity of a parent business.
        While a business can have many revenue centers, a revenue center can roll up to only one business.
        Access to a particular revenue center is determined based on access to the parent business. If an account has access to a parent business, then the consumer has access to data for all revenue centers under the parent business.
      type: object
      required:
        - revenueCenterId
        - revenueCenterName
      properties:
        revenueCenterId:
          type: string
          description: The unique identifier of a revenue center
          example: '5123787'
        revenueCenterName :
          type: string
          description: The name of a revenue center
          example: Bar

    Business:
      description: A business is the first level of an organization.  A business may have one to many revenue centers associated with it.
      type: object
      required:
        - businessId
        - businessName
        - currencyCode
      properties:
        businessId:
          type: string
          description: A unique ID provided to each business. A business is the parent entity to revenue centers.
          example: '7047'
        businessName:
          type: string
          description: The name of the business
          example: Blue Cafe
        currencyCode:
          description: Currency applies to all revenue centers that are underneath a parent business.
          allOf:
            - $ref: '#/components/schemas/CurrencyCode'
        revenueCenters:
          type: array
          description: Revenue centers that are children of the business
          items:
            $ref: '#/components/schemas/RevenueCenter'

    OrganizationLevel:
      description: The organizational structure
      type: object
      required:
        - name
        - level
        - id
      properties:
        name:
          type: string
          description: The name of this level in the organization
        level:
          type: string
          description: The level name in the organizational hierarchy. From least to most granular, they are business, revenueCenter
          enum:
            - business
            - revenueCenter
        id:
          type: string
          description: The identifier of this level in the organization

    OrganizationLevel1:
      description: the nearest organization level
      allOf:
        - $ref: '#/components/schemas/OrganizationLevel'
        - type: object
          properties:
            parent:
              $ref: '#/components/schemas/OrganizationLevel2'
      example:
        level: revenueCenter
        name: Dining Room
        id: '5123787'
        parent:
          level: business
          name: Blue Cafe
          id: '7047'

    OrganizationLevel2:
      description: the 2nd nearest organization level
      allOf:
        - $ref: '#/components/schemas/OrganizationLevel'
      example:
        level: business
        name: Blue Cafe
        id: '7047'

    DecimalAmount:
      type: string
      description: Representation of a positive or negative amount to 2 decimal place precision
      minLength: 4
      pattern: '^((-?(0|[1-9][0-9]*)[.][0-9]{2}))$'
      example: '17919.20'

    CurrencyCode:
      type: string
      description: ISO 4217 3 character currency code
      enum:
        - AED
        - ANG
        - ARS
        - AUD
        - AZN
        - BHD
        - BMD
        - BRL
        - BSD
        - CAD
        - CHF
        - CLP
        - CNY
        - COP
        - CRC
        - CZK
        - DKK
        - DOP
        - EGP
        - EUR
        - GBP
        - GTQ
        - HKD
        - HUF
        - IDR
        - ILS
        - INR
        - JOD
        - JPY
        - KES
        - KRW
        - KWD
        - KYD
        - LBP
        - MAD
        - MMK
        - MOP
        - MUR
        - MXN
        - MYR
        - NZD
        - OMR
        - PEN
        - PHP
        - QAR
        - RUB
        - SAR
        - SCR
        - SGD
        - THB
        - TND
        - TRY
        - TTD
        - USD
        - VND
        - XCD
        - XPF
        - ZAR
      example: USD

    BusinessDay:
      type: string
      description: A business day is the day that the transactions are tied to.
        A business day may cross the boundary of a calendar day.  Business days are in the business's local time zone.
        Business day is tied to the start date of staff shifts according to operators' business schedule and not to the open or close date of checks for a particular date. For example, say a check was opened at 11:59pm on May 29, 2019, but closed at 2:15am on May 30, 2019. That check's sales are considered part of the sales totals for May 29, 2019 since the business operator considers that check part of the 'business day' that started on May 29, 2019.
      format: date
      example: '2019-05-29'

    SummaryMetrics:
      description: A structure to hold summary level metrics
      type: object
      required:
        - grossSales
        - netSales
        - coverCount
        - checkCount
      properties:
        grossSales:
          description: Gross sales is total sales less taxes
          allOf:
            - $ref: '#/components/schemas/DecimalAmount'
        netSales:
          description: Net sales is total sales less taxes and less promotions
          allOf:
            - $ref: '#/components/schemas/DecimalAmount'
        coverCount:
          type: integer
          description: Cover count is the total number of guests
          minimum: 0
          maximum: 2147483647
          example: 474
        checkCount:
          type: integer
          description: Check count is the total number of checks closed
          minimum: 0
          maximum: 2147483647
          example: 254

    SummaryMealSalesAspect:
      description: A structure to hold summary data broken out by meal period
      type: object
      required:
        - name
        - metrics
      properties:
        name:
          type: string
          description: The name of the meal period
          example: Breakfast
        metrics:
          description: The metrics for the meal period
          allOf:
            - $ref: '#/components/schemas/SummaryMetrics'

    SummarySalesAspects:
      description: A structure to hold optional summary sales aspects
      type: object
      properties:
        mealPeriods:
          type: array
          description: An optional aspect that breaks out metrics by meal period
          minLength: 0
          items:
            $ref: '#/components/schemas/SummaryMealSalesAspect'

    SummarySales:
      description: A structure to hold summary sales data
      type: object
      required:
        - organization
        - businessDay
        - currencyCode
        - metrics
      properties:
        organization:
          description: The organization this sales data is attributed to
          allOf:
            - $ref: '#/components/schemas/OrganizationLevel1'
        businessDay:
          description: The business day this sales data is for
          allOf:
            - $ref: '#/components/schemas/BusinessDay'
        currencyCode:
          description: The currency that any money values were transacted
          allOf:
            - $ref: '#/components/schemas/CurrencyCode'
        metrics:
          description: Metrics for this organization, businessDay combination
          allOf:
            - $ref: '#/components/schemas/SummaryMetrics'
        aspects:
          description: Optional aspects for this organization, businessDay combination
          allOf:
            - $ref: '#/components/schemas/SummarySalesAspects'

    SuccessfulResponse:
      description: A standard response object for successful API calls (200)
      type: object
      properties:
        meta:
          type: object

    BusinessResponse:
      description: A response containing businesses
      type: object
      allOf:
        - $ref: '#/components/schemas/SuccessfulResponse'
        - type: object
          properties:
            data:
              type: array
              description: The businesses
              items:
                $ref: '#/components/schemas/Business'

    SummarySalesResponse:
      description: A response containing summary sales
      type: object
      allOf:
        - $ref: '#/components/schemas/SuccessfulResponse'
        - type: object
          properties:
            data:
              type: array
              description: The summary sales
              items:
                $ref: '#/components/schemas/SummarySales'

  parameters:
    optionalBusinessIds:
      name: businessIds
      in: query
      description: Business ids to use. If not provided, will default to all business ids the user has access to.
      required: false
      schema:
        type: array
        items:
          type: string
        minItems: 1
        maxItems: 100
      style: form
      explode: false
    optionalBusinessDays:
      name: businessDays
      in: query
      description: Business days to use. If not provided, will default to yesterday's date.
      required: false
      schema:
        type: array
        items:
          type: string
          format: date
        minItems: 1
        maxItems: 100
      style: form
      explode: false
    optionalSalesAspectsToInclude:
      name: include
      in: query
      description: Optional sales aspects to include in a sales response.  Uses dot notation to specify the inclusion of optional sales aspects objects.
      required: false
      schema:
        type: array
        items:
          type: string
          enum:
            - aspects.mealPeriods
        minItems: 1
        maxItems: 100
      style: form
      explode: false

```