# Economic Data Mining and Analysis of MakerDAO DeFi Project

This research project is to construct a complete dataset from the MakerDAO platform and make it human-readable using Maker's smart contracts. Analyze financial statistics by calculating the interest rate, loss given default, and probability of default. \
The three main things are below:


<!-- and develop a mathematical model designed to estimate the likelihood of default for loans within the MakerDAO ecosystem. This multimodal method seeks to provide useful insights into the risk assessment and lending dynamics of decentralized finance platforms on MakerDAO. -->

- **Create a Comprehensive Dataset:** \
  The first sub-goal is to create a robust dataset encompassing loan portfolios originating from MakerDAO. This dataset will act as the primary source of information for the succeeding phases of the project. It will feature a diversified range of loan portfolios with varying financial characteristics, lending histories, and borrower profiles.

- **Enhance Dataset with Financial features:** \
  The second sub-goal entails enhancing the dataset with essential financial features related to borrowing. Loan amounts, interest rates, collateral kinds, and borrower profiles are examples of these features. This enrichment is critical for a thorough examination of borrowing habits inside the MakerDAO ecosystem.

- **Create and Improve a Specialized Probability of Default Model:** \
  The third sub-objective focuses on the development and improvement of a specialized mathematical model. The goal of this model is to assess and predict
the likelihood of default in the context of MakerDAO's financing activity. The model will combine several parameters based on the enriched dataset to assess the chance of borrowers defaulting on their obligations.

 <img width="1036" alt="Overview" src="https://github.com/Sudarut-kas/Data-Mining-for-MakerDAO/assets/98969542/53a4cadc-d414-4501-b204-1aa401c7dd7d">

 # Paper
 Chaleenutthawut, Y., & Davydov, V. & Evdokimov, M. & Kasemsuk, S. & Kruglik, S. & Melnikov, G. & Yanovich, Y. (2023). ”Loan Portfolio Dataset from MakerDAO Blockchain Project.” Manuscript submitted for publication in the IEEE Journals.

 # How to Install and Run

- Python
- Install web3.0 (for decoding data)
- Install padarellel (save time processing)
- Install sympy (for optimization)
- tqdm
- Numpy
- Pandas
- Matplotlib
- Scipy
- Json

# Usage

Pandarallel will use standard multiprocessing data transfer (pipe) to transfer data between the main process and workers
```python 
from pandarallel import pandarallel
pandarallel.initialize(progress_bar=True, nb_workers=8)
```

# Quick start

Getting data from [Google Biquery](https://cloud.google.com/bigquery?hl=th)\
**Dataset ID:** bigquery-public-data.crypto_ethereum

```sql
/* crypto_ethereum*/
SELECT
        block_timestamp,
        block_number,
        transaction_index,
        trace_address,
        transaction_hash,
        input,
        ARRAY_TO_STRING(
                ARRAY(
                        SELECT CHR(CAST(num AS INT64)) FROM UNNEST(SPLIT(trace_address, ',')) AS num
                ),
                ","
        ) as trace_addr_str
FROM  `bigquery-public-data.crypto_ethereum.traces`
WHERE DATE(block_timestamp) >= "2019-11-12"
        and trace_address IS NOT NULL
        and call_type = "call"
        and to_address = LOWER("0x35D1b3F3D7966A1DFe207aa4514C12a259A0492B")
        and status = 1
ORDER BY CAST(block_number as INT64), CAST(transaction_index as INT64), trace_addr_str

```
# Dataset
MakerDAO dataset from VAT module since the platform started to 31 July 2023
[transaction dataset](https://drive.google.com/file/d/1KJ551BYvw6vVx7pgHYkFPXU9Em0zkHuB/view?usp=share_link)

# Additional
MakerDAO data from smart contracts needs ABIs file to decode the transaction.
You can get into this [MakerDAO Chainlog](https://ipfs.io/ipfs/bafybeid6dreur7nlcuqrdz7irtyffwvt3pvyzvac3cfdxmznw6kmoxmj3a) for any ABI file you want. 

# Article
Loan Portfolio Dataset From MakerDAO Blockchain Project [IEEE](https://ieeexplore.ieee.org/abstract/document/10423641)


# Acknowledgements

Thanks to Yury Yanavich, my supervisor, for supporting the research.

This repository includes adaptations of the following:
- [Makerdao-Risk-Model](https://gitlab.com/gregorymel/makerdao-risk-model/-/blob/master/big_query.sql)
  



