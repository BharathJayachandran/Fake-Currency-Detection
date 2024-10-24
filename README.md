{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "FakeCurrency.ipynb",
      "provenance": []
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "code",
      "metadata": {
        "id": "B75QTdSpKLFq"
      },
      "source": [
        "import pandas as pd\n",
        "import numpy as np\n",
        "import matplotlib.pyplot as plt\n",
        "import seaborn as sns"
      ],
      "execution_count": 1,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "isrmGMRLGRBS",
        "outputId": "1e967b48-1b04-4176-d743-400f72e0c3d3"
      },
      "source": [
        "from google.colab import drive\n",
        "drive.mount(\"/content/gdrive\")\n"
      ],
      "execution_count": 2,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Drive already mounted at /content/gdrive; to attempt to forcibly remount, call drive.mount(\"/content/gdrive\", force_remount=True).\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "iY_9a8NFGgTZ"
      },
      "source": [
        "df = pd.read_csv('/content/gdrive/My Drive/DataSets/banknotes.csv')"
      ],
      "execution_count": 3,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "V8qEvwf3Gd9s",
        "outputId": "2a9b2c52-140a-4584-83ad-4136ab62f544"
      },
      "source": [
        "df.head"
      ],
      "execution_count": 4,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<bound method NDFrame.head of      conterfeit  Length   Left  Right  Bottom   Top  Diagonal\n",
              "0             0   214.8  131.0  131.1     9.0   9.7     141.0\n",
              "1             0   214.6  129.7  129.7     8.1   9.5     141.7\n",
              "2             0   214.8  129.7  129.7     8.7   9.6     142.2\n",
              "3             0   214.8  129.7  129.6     7.5  10.4     142.0\n",
              "4             0   215.0  129.6  129.7    10.4   7.7     141.8\n",
              "..          ...     ...    ...    ...     ...   ...       ...\n",
              "195           1   215.0  130.4  130.3     9.9  12.1     139.6\n",
              "196           1   215.1  130.3  129.9    10.3  11.5     139.7\n",
              "197           1   214.8  130.3  130.4    10.6  11.1     140.0\n",
              "198           1   214.7  130.7  130.8    11.2  11.2     139.4\n",
              "199           1   214.3  129.9  129.9    10.2  11.5     139.6\n",
              "\n",
              "[200 rows x 7 columns]>"
            ]
          },
          "metadata": {},
          "execution_count": 4
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 202
        },
        "id": "M-kMJ2UYHaez",
        "outputId": "78bcec18-869e-4323-ce97-aad230413abe"
      },
      "source": [
        "df.head()"
      ],
      "execution_count": 5,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>conterfeit</th>\n",
              "      <th>Length</th>\n",
              "      <th>Left</th>\n",
              "      <th>Right</th>\n",
              "      <th>Bottom</th>\n",
              "      <th>Top</th>\n",
              "      <th>Diagonal</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>0</td>\n",
              "      <td>214.8</td>\n",
              "      <td>131.0</td>\n",
              "      <td>131.1</td>\n",
              "      <td>9.0</td>\n",
              "      <td>9.7</td>\n",
              "      <td>141.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>0</td>\n",
              "      <td>214.6</td>\n",
              "      <td>129.7</td>\n",
              "      <td>129.7</td>\n",
              "      <td>8.1</td>\n",
              "      <td>9.5</td>\n",
              "      <td>141.7</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>0</td>\n",
              "      <td>214.8</td>\n",
              "      <td>129.7</td>\n",
              "      <td>129.7</td>\n",
              "      <td>8.7</td>\n",
              "      <td>9.6</td>\n",
              "      <td>142.2</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>0</td>\n",
              "      <td>214.8</td>\n",
              "      <td>129.7</td>\n",
              "      <td>129.6</td>\n",
              "      <td>7.5</td>\n",
              "      <td>10.4</td>\n",
              "      <td>142.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>0</td>\n",
              "      <td>215.0</td>\n",
              "      <td>129.6</td>\n",
              "      <td>129.7</td>\n",
              "      <td>10.4</td>\n",
              "      <td>7.7</td>\n",
              "      <td>141.8</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   conterfeit  Length   Left  Right  Bottom   Top  Diagonal\n",
              "0           0   214.8  131.0  131.1     9.0   9.7     141.0\n",
              "1           0   214.6  129.7  129.7     8.1   9.5     141.7\n",
              "2           0   214.8  129.7  129.7     8.7   9.6     142.2\n",
              "3           0   214.8  129.7  129.6     7.5  10.4     142.0\n",
              "4           0   215.0  129.6  129.7    10.4   7.7     141.8"
            ]
          },
          "metadata": {},
          "execution_count": 5
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 294
        },
        "id": "hCinD28LHczg",
        "outputId": "26b54c0b-0251-4556-eeae-74b21da824f7"
      },
      "source": [
        "df.describe()"
      ],
      "execution_count": 6,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>conterfeit</th>\n",
              "      <th>Length</th>\n",
              "      <th>Left</th>\n",
              "      <th>Right</th>\n",
              "      <th>Bottom</th>\n",
              "      <th>Top</th>\n",
              "      <th>Diagonal</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>200.000000</td>\n",
              "      <td>200.000000</td>\n",
              "      <td>200.000000</td>\n",
              "      <td>200.000000</td>\n",
              "      <td>200.000000</td>\n",
              "      <td>200.000000</td>\n",
              "      <td>200.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>mean</th>\n",
              "      <td>0.500000</td>\n",
              "      <td>214.896000</td>\n",
              "      <td>130.121500</td>\n",
              "      <td>129.956500</td>\n",
              "      <td>9.417500</td>\n",
              "      <td>10.650500</td>\n",
              "      <td>140.483500</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>std</th>\n",
              "      <td>0.501255</td>\n",
              "      <td>0.376554</td>\n",
              "      <td>0.361026</td>\n",
              "      <td>0.404072</td>\n",
              "      <td>1.444603</td>\n",
              "      <td>0.802947</td>\n",
              "      <td>1.152266</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>min</th>\n",
              "      <td>0.000000</td>\n",
              "      <td>213.800000</td>\n",
              "      <td>129.000000</td>\n",
              "      <td>129.000000</td>\n",
              "      <td>7.200000</td>\n",
              "      <td>7.700000</td>\n",
              "      <td>137.800000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>25%</th>\n",
              "      <td>0.000000</td>\n",
              "      <td>214.600000</td>\n",
              "      <td>129.900000</td>\n",
              "      <td>129.700000</td>\n",
              "      <td>8.200000</td>\n",
              "      <td>10.100000</td>\n",
              "      <td>139.500000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>50%</th>\n",
              "      <td>0.500000</td>\n",
              "      <td>214.900000</td>\n",
              "      <td>130.200000</td>\n",
              "      <td>130.000000</td>\n",
              "      <td>9.100000</td>\n",
              "      <td>10.600000</td>\n",
              "      <td>140.450000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>75%</th>\n",
              "      <td>1.000000</td>\n",
              "      <td>215.100000</td>\n",
              "      <td>130.400000</td>\n",
              "      <td>130.225000</td>\n",
              "      <td>10.600000</td>\n",
              "      <td>11.200000</td>\n",
              "      <td>141.500000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>max</th>\n",
              "      <td>1.000000</td>\n",
              "      <td>216.300000</td>\n",
              "      <td>131.000000</td>\n",
              "      <td>131.100000</td>\n",
              "      <td>12.700000</td>\n",
              "      <td>12.300000</td>\n",
              "      <td>142.400000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "       conterfeit      Length        Left  ...      Bottom         Top    Diagonal\n",
              "count  200.000000  200.000000  200.000000  ...  200.000000  200.000000  200.000000\n",
              "mean     0.500000  214.896000  130.121500  ...    9.417500   10.650500  140.483500\n",
              "std      0.501255    0.376554    0.361026  ...    1.444603    0.802947    1.152266\n",
              "min      0.000000  213.800000  129.000000  ...    7.200000    7.700000  137.800000\n",
              "25%      0.000000  214.600000  129.900000  ...    8.200000   10.100000  139.500000\n",
              "50%      0.500000  214.900000  130.200000  ...    9.100000   10.600000  140.450000\n",
              "75%      1.000000  215.100000  130.400000  ...   10.600000   11.200000  141.500000\n",
              "max      1.000000  216.300000  131.000000  ...   12.700000   12.300000  142.400000\n",
              "\n",
              "[8 rows x 7 columns]"
            ]
          },
          "metadata": {},
          "execution_count": 6
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "1ZET81tiHhX3",
        "outputId": "77edfb5f-b466-4afe-b4f6-35383823d985"
      },
      "source": [
        "df.info()"
      ],
      "execution_count": 7,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "RangeIndex: 200 entries, 0 to 199\n",
            "Data columns (total 7 columns):\n",
            " #   Column      Non-Null Count  Dtype  \n",
            "---  ------      --------------  -----  \n",
            " 0   conterfeit  200 non-null    int64  \n",
            " 1   Length      200 non-null    float64\n",
            " 2   Left        200 non-null    float64\n",
            " 3   Right       200 non-null    float64\n",
            " 4   Bottom      200 non-null    float64\n",
            " 5   Top         200 non-null    float64\n",
            " 6   Diagonal    200 non-null    float64\n",
            "dtypes: float64(6), int64(1)\n",
            "memory usage: 11.1 KB\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 324
        },
        "id": "idxUCQU9HhaT",
        "outputId": "4c320c76-2609-4f27-cc5c-892769def028"
      },
      "source": [
        "sns.heatmap(df.isnull())\n",
        "plt.title(\"Missing values?\", fontsize = 18)\n",
        "plt.show()"
      ],
      "execution_count": 8,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "image/png":![1](https://github.com/user-attachments/assets/7fe64870-8faa-46b2-902f-e242e2561119)
