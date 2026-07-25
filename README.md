# MoMoTrack NER v1

A fine-tuned **DistilBERT** Named Entity Recognition (NER) model for extracting structured information from **Ghanaian Mobile Money (MoMo) SMS messages**.

The model is designed to power **MoMoTrack**, an AI-driven personal finance application that automatically parses MoMo SMS messages, extracts transaction details, and converts them into structured financial records.

---

## Features

The model extracts the following entities:

- 💰 Amounts
- 💳 Account Balances
- 👤 Counterparties (Senders/Recipients)
- 🆔 Transaction IDs
- 💸 Charges & Fees
- 📄 References

Supported transaction types include:

- Money Sent
- Money Received
- Cash In
- Cash Out
- Airtime Purchases
- Merchant Payments
- Bank Transfers
- Other Mobile Money transaction messages

The model also learns to ignore promotional, informational, and non-transactional SMS messages.

---

## Model

- **Base Model:** DistilBERT
- **Task:** Named Entity Recognition (NER)
- **Language:** English
- **Domain:** Ghanaian Mobile Money SMS

---

## Validation Performance

| Metric | Score |
|--------|------:|
| Precision | **87.60%** |
| Recall | **92.03%** |
| F1 Score | **89.76%** |
| Accuracy | **94.74%** |

---

## Example

### Input

```text
Cash In received for GHS 5.00 from DAV ENTERPRISE.
Current Balance GHS 10.00.
Available Balance GHS 10.00.
Transaction ID: 85197913453.
Fee charged: GHS 0.00.
```

### Output

```json
{
  "AMOUNT": "GHS 5.00",
  "COUNTERPARTY": "DAV ENTERPRISE",
  "BALANCE": [
    "GHS 10.00",
    "GHS 10.00"
  ],
  "TXN_ID": "85197913453",
  "CHARGES": "GHS 0.00"
}
```


---

## Current Limitations

This is the first public release (**v1**).

Known limitations include:

- Some entities may be split into multiple tokens (for example, transaction IDs and monetary values).
- Entity normalization (e.g., `GHS 10 . 00 → GHS 10.00`) should be handled during post-processing.
- Some metadata fields may require additional business rules after extraction.
- Performance may vary on previously unseen SMS formats.

---

## Future Improvements

Planned improvements for future versions include:

- Improved entity boundary detection
- Better handling of complex transaction IDs
- Support for additional Mobile Money providers
- Expanded training dataset
- More transaction entity types
- Higher precision on edge cases

---

## License

This project is licensed under the **Apache License 2.0**.

The model is fine-tuned from **DistilBERT**, originally developed by **Hugging Face**, which is also distributed under the **Apache License 2.0**.

---

## Acknowledgements

- Hugging Face
- DistilBERT
- PyTorch
- Transformers
- seqeval

---

## Author

**Ahmed Mohammed**

Built as part of the **MoMoTrack** project to make Mobile Money transaction tracking faster, smarter, and fully automated.
