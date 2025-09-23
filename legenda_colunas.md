# Legenda para as colunas do datasets

Apenas as features marcadas com * serão mantidas para treinamento para evitar sobrecarga e redundância do modelo.

| Key        | Description                                                                 | Marcação|
|------------|-----------------------------------------------------------------------------|---------|
| Div        | League Division                                                             |    *    |
| Date       | Match Date (dd/mm/yy)                                                       |    *    |
| Time       | Time of match kick off                                                      |    *    |
| HomeTeam   | Home Team                                                                   |    *    |
| AwayTeam   | Away Team                                                                   |    *    |
| FTHG / HG  | Full Time Home Team Goals                                                   |    *    |
| FTAG / AG  | Full Time Away Team Goals                                                   |    *    |
| FTR / Res  | Full Time Result (H=Home Win, D=Draw, A=Away Win)                           |    *    |
| HTHG       | Half Time Home Team Goals                                                   |    *    |
| HTAG       | Half Time Away Team Goals                                                   |    *    |
| HTR        | Half Time Result (H=Home Win, D=Draw, A=Away Win)                           |    *    |
| Referee    | Match Referee                                                               |    *    |
| HS         | Home Team Shots                                                             |    *    |
| AS         | Away Team Shots                                                             |    *    |
| HST        | Home Team Shots on Target                                                   |    *    |
| AST        | Away Team Shots on Target                                                   |    *    |
| HC         | Home Team Corners                                                           |    *    |
| AC         | Away Team Corners                                                           |    *    |
| HF         | Home Team Fouls Committed                                                   |    *    |
| AF         | Away Team Fouls Committed                                                   |    *    |
| HY         | Home Team Yellow Cards                                                      |    *    |
| AY         | Away Team Yellow Cards                                                      |    *    |
| HR         | Home Team Red Cards                                                         |    *    |
| AR         | Away Team Red Cards                                                         |    *    |
| B365H      | Bet365 home win odds                                                        |    *    |
| B365D      | Bet365 draw odds                                                            |    *    |
| B365A      | Bet365 away win odds                                                        |    *    |
| BWH        | Bet&Win home win odds                                                       |         |
| BWD        | Bet&Win draw odds                                                           |         |
| BWA        | Bet&Win away win odds                                                       |         |
| IWH        | Interwetten home win odds                                                   |         |
| IWD        | Interwetten draw odds                                                       |         |
| IWA        | Interwetten away win odds                                                   |         |
| PSH / PH   | Pinnacle home win odds                                                      |    *    |
| PSD / PD   | Pinnacle draw odds                                                          |    *    |
| PSA / PA   | Pinnacle away win odds                                                      |    *    |
| VCH        | VC Bet home win odds (now BetVictor)                                        |         |
| VCD        | VC Bet draw odds (now BetVictor)                                            |         |
| VCA        | VC Bet away win odds (now BetVictor)                                        |         |
| WHH        | William Hill home win odds                                                  |         |
| WHD        | William Hill draw odds                                                      |         |
| WHA        | William Hill away win odds                                                  |         |
| MaxH       | Market maximum home win odds                                                |    *    |
| MaxD       | Market maximum draw win odds                                                |    *    |
| MaxA       | Market maximum away win odds                                                |    *    |
| AvgH       | Market average home win odds                                                |    *    |
| AvgD       | Market average draw win odds                                                |    *    |
| AvgA       | Market average away win odds                                                |    *    |
| B365>2.5   | Bet365 over 2.5 goals                                                       |    *    |
| B365<2.5   | Bet365 under 2.5 goals                                                      |    *    |
| P>2.5      | Pinnacle over 2.5 goals                                                     |    *    |
| P<2.5      | Pinnacle under 2.5 goals                                                    |    *    |
| Max>2.5    | Market maximum over 2.5 goals                                               |    *    |
| Max<2.5    | Market maximum under 2.5 goals                                              |    *    |
| Avg>2.5    | Market average over 2.5 goals                                               |    *    |
| Avg<2.5    | Market average under 2.5 goals                                              |    *    |
| AHh        | Market size of handicap (home team) (since 2019/2020)                       |         |
| B365AHH    | Bet365 Asian handicap home team odds                                        |    *    |
| B365AHA    | Bet365 Asian handicap away team odds                                        |    *    |
| PAHH       | Pinnacle Asian handicap home team odds                                      |    *    |
| PAHA       | Pinnacle Asian handicap away team odds                                      |    *    |
| MaxAHH     | Market maximum Asian handicap home team odds                                |    *    |
| MaxAHA     | Market maximum Asian handicap away team odds                                |    *    |
| AvgAHH     | Market average Asian handicap home team odds                                |    *    |
| AvgAHA     | Market average Asian handicap away team odds                                |    *    |
