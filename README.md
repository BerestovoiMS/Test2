{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import redis as rd"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [
    {
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
       "      <th>town1</th>\n",
       "      <th>Avg-Avg-К9</th>\n",
       "      <th>Avg-Avg-К101</th>\n",
       "      <th>Avg-Avg-К102</th>\n",
       "      <th>Avg-Avg-К11</th>\n",
       "      <th>Avg-Avg-К121</th>\n",
       "      <th>Avg-Avg-К122</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Абакан</td>\n",
       "      <td>703.500000</td>\n",
       "      <td>94.250000</td>\n",
       "      <td>0.750000</td>\n",
       "      <td>6.750000</td>\n",
       "      <td>5.250000</td>\n",
       "      <td>1.250000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Азовский район</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Аксайский район</td>\n",
       "      <td>6.250000</td>\n",
       "      <td>8.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>1.500000</td>\n",
       "      <td>1.500000</td>\n",
       "      <td>0.250000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Алексеевкий район</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Анапа</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>276</th>\n",
       "      <td>Южно-Сахалинск</td>\n",
       "      <td>62.450000</td>\n",
       "      <td>12.450000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.450000</td>\n",
       "      <td>0.850000</td>\n",
       "      <td>0.200000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>277</th>\n",
       "      <td>Якутск</td>\n",
       "      <td>67.400000</td>\n",
       "      <td>27.650000</td>\n",
       "      <td>0.366667</td>\n",
       "      <td>2.750000</td>\n",
       "      <td>2.250000</td>\n",
       "      <td>0.550000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>278</th>\n",
       "      <td>Ялта</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>2.666667</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.500000</td>\n",
       "      <td>0.833333</td>\n",
       "      <td>0.166667</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>279</th>\n",
       "      <td>Ярославль</td>\n",
       "      <td>299.404762</td>\n",
       "      <td>62.500000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>5.964286</td>\n",
       "      <td>7.107143</td>\n",
       "      <td>1.535714</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>280</th>\n",
       "      <td>Ярославский район</td>\n",
       "      <td>7.333333</td>\n",
       "      <td>5.000000</td>\n",
       "      <td>0.666667</td>\n",
       "      <td>1.666667</td>\n",
       "      <td>0.333333</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>281 rows × 7 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                 town1  Avg-Avg-К9  Avg-Avg-К101  Avg-Avg-К102  Avg-Avg-К11  \\\n",
       "0               Абакан  703.500000     94.250000      0.750000     6.750000   \n",
       "1       Азовский район    0.000000      0.000000      0.000000     0.000000   \n",
       "2      Аксайский район    6.250000      8.000000      0.000000     1.500000   \n",
       "3    Алексеевкий район    0.000000      0.000000      0.000000     0.000000   \n",
       "4                Анапа    0.000000      0.000000      0.000000     0.000000   \n",
       "..                 ...         ...           ...           ...          ...   \n",
       "276     Южно-Сахалинск   62.450000     12.450000      0.000000     0.450000   \n",
       "277             Якутск   67.400000     27.650000      0.366667     2.750000   \n",
       "278               Ялта    0.000000      2.666667      0.000000     0.500000   \n",
       "279          Ярославль  299.404762     62.500000      1.000000     5.964286   \n",
       "280  Ярославский район    7.333333      5.000000      0.666667     1.666667   \n",
       "\n",
       "     Avg-Avg-К121  Avg-Avg-К122  \n",
       "0        5.250000      1.250000  \n",
       "1        0.000000      0.000000  \n",
       "2        1.500000      0.250000  \n",
       "3        0.000000      0.000000  \n",
       "4        0.000000      0.000000  \n",
       "..            ...           ...  \n",
       "276      0.850000      0.200000  \n",
       "277      2.250000      0.550000  \n",
       "278      0.833333      0.166667  \n",
       "279      7.107143      1.535714  \n",
       "280      0.333333      0.000000  \n",
       "\n",
       "[281 rows x 7 columns]"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "D = pd.read_excel(\"https://github.com/junaart/ForStudents/raw/refs/heads/main/R/Zachet/DataSets/2.xlsx\")\n",
    "display(D)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['town1', 'Avg-Avg-К9', 'Avg-Avg-К101', 'Avg-Avg-К102', 'Avg-Avg-К11',\n",
       "       'Avg-Avg-К121', 'Avg-Avg-К122'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "D.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "r = rd.Redis (host='localhost', db=0)\n",
    "key = \"A1\"\n",
    "for i in range(len(D[\"Avg-Avg-К9\"])):\n",
    "    r.set(key+str(i),str(D[\"Avg-Avg-К9\"].iloc[i]))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [],
   "source": [
    "r = rd.Redis (host='localhost', db=0)\n",
    "key = \"A2\"\n",
    "for i in range(len(D[\"Avg-Avg-К101\"])):\n",
    "    r.set(key+str(i),str(D[\"Avg-Avg-К101\"].iloc[i]))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [],
   "source": [
    "r = rd.Redis (host='localhost', db=0)\n",
    "key = \"A3\"\n",
    "for i in range(len(D[\"Avg-Avg-К102\"])):\n",
    "    r.set(key+str(i),str(D[\"Avg-Avg-К102\"].iloc[i]))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [],
   "source": [
    "r = rd.Redis (host='localhost', db=0)\n",
    "key = \"A4\"\n",
    "for i in range(len(D[\"Avg-Avg-К11\"])):\n",
    "    r.set(key+str(i),str(D[\"Avg-Avg-К11\"].iloc[i]))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [],
   "source": [
    "r = rd.Redis (host='localhost', db=0)\n",
    "key = \"A5\"\n",
    "for i in range(len(D[\"Avg-Avg-К121\"])):\n",
    "    r.set(key+str(i),str(D[\"Avg-Avg-К121\"].iloc[i]))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [],
   "source": [
    "r = rd.Redis (host='localhost', db=0)\n",
    "key = \"A6\"\n",
    "for i in range(len(D[\"Avg-Avg-К122\"])):\n",
    "    r.set(key+str(i),str(D[\"Avg-Avg-К122\"].iloc[i]))"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.12.1"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
