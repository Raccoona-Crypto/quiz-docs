# Quiz service API Documentation

### 1. QuizPhrase format
QuizPhrase is a unique list of words separated by space. Each word has to be lowercased, with any meaning and length, contained by symbols `[a-z], [а-я]` and digits. QuizPhrase can be 4 words minimun.

**Examples**
```
quize 9083 kilovay puppy over9000

lol watter bitcoin plark awesome quiz quiz a superthot
```


### 2. Check QuizPhrase

**Request**
```bash
POST /quiz/check
```

```json
{
  "quizPhrase": "lol watter bitcoin plark awesome"
}
```

**✅ Response if Phrase exists and ready to redeem**
```
HTTP 200
```
```bash
{
  "currency": "BTC",    # cryptocurrency asset (BTC, DASH, ETH, etc.)
  "amount": 0.002924    # amount
}
```

**❌ Response if Phrase exists and already redeemed/expired**
```bash
HTTP 400: QuizPhrase expired
HTTP 400: QuizPhrase redeemed
```

**❌ Response if Phrase not exists**
```bash
HTTP 404: QuizPhrase not found
```

**❌ Response if out of limit (anti spam)**
```bash
HTTP 429: Out of limit
```


### 3. Redeem QuizPhrase

**Request**
```bash
POST /quiz/redeem
```

```bash
{
  "quizPhrase": "lol watter bitcoin plark awesome",   # QuizPhrase
  "address": "1kd72...."                              # Bitcoin address
}
```

**✅ Response if successful redeemed**
```
HTTP 200
```
```bash
{
  "txid": "as834jcx989dfsdf..." # TXID of transansation
  "currency": "BTC"
}
```

**❌ Responses on error**
```bash
HTTP 400: Invalid address
HTTP 400: QuizPhrase already redeemed
HTTP 404: QuizPhrase does not exists
```

### 4. Check status

**Request**
```bash
GET /quiz/status
```

**✅ Response if Phrase exists and ready to redeem**
```
HTTP 200
```
```bash
{
  "ok": true
}
```
