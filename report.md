# Lab 01 — The Price of One Request

## 1. Prediction and measured results

Before measuring the complaint, I predicted that the Russian and Kazakh versions would require more tokens than the English version. My prediction was based mainly on the difference in text representation and tokenization, rather than only on the number of words.

| Language | Prediction vs EN | Measured input-token ratio |
|---|---:|---:|
| English | 1.00× | 1.00× |
| Russian | ~1.5× | 1.44× |
| Kazakh | ~2.0× | 2.19× |

The measured results show that the prediction was reasonably close. Russian required about 1.44 times as many input tokens as English, while Kazakh required about 2.19 times as many. This demonstrates that token cost depends on tokenization, not simply on the number of words or characters.

For the current calculation, I used the reference measurements provided with the lab because the instructor's API key was not available. The README specifies that `measurements.example.json` is a reference run that can be used when the projector key is unavailable.

## 2. Annual cost

I used a volume of **2,000 support requests per day** because this represents a moderate support queue and makes the annual difference between languages and models visible.

### Annual cost at 2,000 requests/day

| Model | English | Russian | Kazakh |
|---|---:|---:|---:|
| Haiku-4.5 | $3,592 | $4,627 | $5,111 |
| Sonnet-5 | $7,183 | $9,255 | $10,223 |
| Opus-5 | $17,958 | $23,137 | $25,557 |
| Fable-5.1 | $35,916 | $46,275 | $51,115 |

The input-token ratio and the final bill ratio are not identical because the total cost also depends on output tokens. For example, for Opus-5, using Russian instead of English increases the annual bill from $17,958 to $23,137, while Kazakh increases it to $25,557.

The reference results give total-bill ratios of **1.29× for Russian** and **1.42× for Kazakh** relative to English on Opus-5.

## 3. Model for a Kazakh-language support queue

For a production Kazakh-language support queue, I would choose **Haiku-4.5** if the main requirement is to handle a large number of routine support requests while keeping the cost relatively low.

At 2,000 requests per day, the reference annual cost for Kazakh is approximately **$5,111** with Haiku-4.5, compared with **$10,223** for Sonnet-5 and **$25,557** for Opus-5.

The quality side also matters. A more expensive model may be useful when a request requires more complex reasoning, but for a routine support queue the additional model capability should be justified by a measurable quality improvement. Therefore, I would use the lower-cost model for routine cases and consider a more capable model for cases that need escalation.

## 4. Cost-reduction lever

One cost-reduction lever not used by this lab is **prompt caching**: the repeated system prompt could be cached so that the same instructions do not have to be paid for at the normal input-token rate on every request.

## AI-use declaration

I used AI to better understand the assignment instructions and clarify the structure of the laboratory task. It was also used to clarify when to start preparing the report.