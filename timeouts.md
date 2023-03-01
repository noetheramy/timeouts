# Disconnection Categories and Abandonment Penalty 

<br>

## Table of Contents
[1. Context](#1-context)  
[2. Business Objectives](#2-business-objectives)  
[3. RICE](#3-rice)  
[4. Success Metrics](#4-success-metrics)  
[5. Features](#5-features)  
[6. Assumptions, Constraints, General Requirements](#6-assumptions-constraints-general-requirements)  
[7. Discussion](#7-discussion)  
[8. Timelines and release planing](#8-timelines-and-release-planing)  
[9. В двух словах](#9-в-двух-словах)  

<br>

## 1. Context

1. Among all product metrics one is the *timeout-rate*, which is the percent of games ended up with the looser not taking any steps for too long.
2. Attributing to cash games only, one can find this metrics being equal to 2.5%.
3. Common cases and reasons for a timeout are:
    1. Technical drawbacks of the app (crashes, network errors, etc.); logical collisions from being not properly worked out by creators; user-unfriendliness:
        1. In this case, the winner and the looser both get frustrated; it is a costful system behavior preferred to be avoided by all means.
    2. Behavioural traits of players, pursuing their own benefits in order to win the game; or players abandoning games in their impulsiveness or indifference:  
        1. In this case, the rightful winner gets frustrated and can sometimes even surrender, and the intruder gets away being encouraged to continue his misbehavior;
        2. Auto-losing on disconnection is far too strict system response, not giving the troubled player any ability to reconnect and restore the game. This can be easily interpreted by users as a consequence of ill-concieving and user-unfriendliness of the app.
4. Thus the main danger enclosed in timeout-situations is they provoke unnessessary raise in churn-rate caused by the unfair game loose:
    1. for winner: they possibly accompanied by very long and annoying waiting time they need to pass through to win the game, otherwise surrender unfairly;
    2. for looser: they possibly accompanied by unfair loose not because of skills but because of poor network quality.
5. In any scenario, a high level of timeouts is likely to contribute to low players loyalty and hence low retertion-rate, RR.
6. However, the only way the system can adjust timeouts is the timebank, determining when the game becomes technically finished.
    1. ~~The club directors can be assigned to resolve doubtable situations, but it seem like a whole new feature with timeouts being just one particular case.~~ 

## 2. Business Objectives

> ---  
> 
> We are not to lower the overall percent of timeouts - as we cannot prevent users from leaving if they want.  
> 
> **We are to lower**:  
>    - **the percent of unjustified timeouts** - as we, though, do can give the reliable users an opportunity to win instantly over leavers (and even prevent leavers from playing with non-leavers);
>    - **to lower expectation time needed to win technically** - we can manage the time required from users to gain their earned victory.  
> 
> 'Disconnection Categories' and 'Abandonment Penalty' are basically two alternatives solving the problem. Here we focus on Disconnection Categories because of its simplicity and consequent cost-effectiveness, but will also touch the subject of possible application of Abandonment Penalty.  
> 
> ---   

<br>

1. 'Disconnection Categories' decomposition:  
    **1.** Distinguish between 'leavers' and 'decent' (non-leavers with good connection);  
    **2.** Make leavers loose faster or immediately;  
    **3.** Make sure disconnected 'decent' users (non-leavers) have their time and do not loose immediately (only possible in case of good latency statistics).
<br>  

2. To Backlog:  
    **-** Distinguish users with poor connection from leavers and disconnection-abusers (for now we assume it is impossible); reveal detailed traits of leavers (winrate, percent of timeouts, moving average latency over the last 20 games, etc.) in order to stop mixing them up.  
    **-** Make matchmaking more like "stable vs stable" and "poor vs poor".  
    **-** Introduce extra-punishment for leavers, more severe as compared with surrenders (for surrender it is nothing at all) - in order to foster surrendering and further reduce the number of leavers.

## 3. RICE

RICE = **10** * **1** * **1** / **1** = **10**.

After normalization RICE to the auditory size (50):  
Final **RICE = 0.2 * total users**

### RICE - Reach

Target demographics are those users who happened:
1. to win in timeout-matches, with time being up;
2. to loose in timeout-matches, surrendering directly of their own free will, while the opponent's disconnection countdown was active;
3. to play, staying connected, with a user being regularly disconnected: even if the game ends up with koks/oin/mars this is still highly likely to be a disconnection-abuse situation. Although a successfull abuse usually would be a *stable* vs *poor* match with the *stable* user losing, let us consider all the situations of *stable* vs *poor* matches are the target ones.  

Let us assume:  
- **Total number of users = 50**;  
- **Total number of matches = 1000**;  
- **The system is now holding 200 matches per month**.  

*The numbers are deliberately exaggerated.*  
*May we have only one leaver, the number of his victims  can still be significant.*  

| Category                                     | Number of matches | % of matches | Share of unique users |
| -------------------------------------------- | ----------------- | ------------ | --------------------- |
| Timeouts                                     | 25                | 2.5          | **10** (ad lib)       |
| Surrenderings while opponent is disconnected | 50                | 5            | **10** (ad lib)       |
| Koks/oin/mars with disconnection of looser   | 100               | 10           | **10** (ad lib)       |
  
Thence the target audience size can vary from 10 to 30 users out of 50, that is 20-60%, even talking about small timeframes, like months or weeks.  

Let's assume for our case **target audience size is 10 users**, or 20% of the total number of users.   

### RICE - Impact

- 3 = massive impact
- 2 = high impact
- **1 = medium impact**
- .5 = low impact
- .25 = minimal impact

### RICE - Confidence

- **100% = high confidence**
- 80% = medium confidence
- 50% = low confidence

### RICE - Effort

| Resourse                         | Days/Hours/SP/etc. | Comment |
| -------------------------------- | ------------------ | ------- |
| product                          | 2d                 | spent   |
| analytics                        | 1d                 |         |
| design                           | -                  |         |
| architecture                     | .5d                |         |
| web-developing front-end         | -                  |         |
| mobile development (android)     | -                  |         |
| mobile development (iOS)         | 1w                 |         |
| developing back-end              | 1w                 |         |
| engineering                      | -                  |         |
| mobile testing                   | 2d                 |         |
| web-testing UI                   | 2d                 |         |
| testing back-end ()              | 2d                 |         |
| integration, fixing bugs, retest | 1w                 |         |
| total number of resources        | **~4w**            |         |

**This gives us 1 person-month**.

## 4. Success Metrics

Conditional timeout-rate:  
- % of timeouts in the group of users with average latency over last 20 games being less than 200 ms (group of well-established network connection).

| Time     | Value |
| -------- | ----- |
| Now      | 2.5%  |
| Expected | 0.5%  |

## 5. Features

### Disconnection Categories

Splitting all users in 2 categories:
- average latency over last 20 games <= 200 ms;
- average latency over last 20 games > 200 ms;

### Abandonment Penalty

'Abandonment Penalty' feature is basically an alternative to 'Disconnection Categories' and can be used to tune user's timebank precisely on the basis of a complex score (representing the probability of this user being leaver or abuser).

- Users have a timebank = 60 sec (initially) - this is the time amount that can be potentially spent on being disconnected.
- Users possess a new metrics 'Abandonment Penalty' which is the number of timeouts (technical victories + technical defeats) out of their 10/20/50/100 last matches;
- For each timeout in their game history, players lose some amount of time from their timebank.
- The further a timeout is located in the game history, the smaller its impact on the player's timebank.  
- There is no need in tracking users' latencies.

For example:
- For each game abandoned among the last 10 ones, player loses 10 sec. from his timebank until it reaches the minimum of 10 sec.
- If a player has not abandoned any games out of the last 5 ones, his timebank restores 10 second for each extra one in a row.

| Feature                       | Pros                                           | Cons                                                                  |
| ----------------------------- | ---------------------------------------------- | --------------------------------------------------------------------- |
| 'Disconnection<br>Categories' | - NO user's timeout statictics<br>- Simplicity | - Latency needed<br>- Segregating users<br>- System can be too strict |
| 'Abandonment<br>Penalty'      | - NO user's latency statictics<br>- Leavers and ordinary players are trated identically | - Need to track technical victories and defeats<br>- The penalty metrics should be properly adjusted<br>- System can be too permissive |

## 6. Assumptions, Constraints, General Requirements

~~A player does have a number of legal timeouts. After they are over, he looses game if time is up.~~ 

1. A player does not always know wheather his Internet connection is good enough or not.
2. A player's bad connection should be highlighted to both sides in advance.
3. App crashes are minimized to lowest possible level: percentage of users without crashes ever is >= 98% (% of users without crashes can be estimated through the insturumets of reports on  failure / halting / errors).
4. The ping (the latency) is considered to be good if it is below 50 ms, normal ping is up to 100–150 ms; ping of 500 ms is uncomfortable and inconvenient for users.
5. A player has an attribute called 'timebank' (or maybe disconnect-bank, or like).
6. Timebank is initially 60 sec.
7. If timebank is up, the disconnected player looses the match technically. 
8. Player's timebank can be shortened up to 10 sec.
9. Timeout bank cannot exceed 60 seconds.
10. Players have a metrics of average latency over their last 20 matches.
11. Player can be whether in 'decent' group or in 'leavers' group.
12. If a player's average latency over last 20 matches exceeds 200ms, they will remain or will be moved to the 'leavers' group.
13. If a player's average latency over last 20 matches falls below 200ms, they will remain or will be moved to the 'decent' group.
14. The latency for a match must be the biggest latency recorded for a player during the whole match, including the time being disconnected.
15. If there any categorical statistics on the winrate, the priority of victories should be considered as follows:
    - technical victory > koks > mars > oin.
16. The player connot start a new game without admitting he has lost the previous match (the system may just informs users on that they had lost previous match whilst joining a new one), including the app re-launch. 
17. The system should NOT punish players leaving the game intentionally with UI (surrendering).
18. The system should NOT punish players leaving the game because of network disconnection if they are 'decent'.  
19. We can hardly influence the number of players with poor network quality.
20. We can influence the number of players abandoning the game because it becomes senseless: the probability of their opponent tilting and surrender in 10 second getting closer to 0%.

## 7. Discussion

| Still opened questions | Likely answers |
| ---------------------- | -------------- |
| 1. Does the lower timeout-rate leads to lower retention-rate?<br>What is the coefficent of correlation between retention-rate and timeout-rate?<br>Do we need to lower timeout-rate? | Let us assume YES here (A/B test needed).<br>Let us assume it is significant enough, may be 0.4 or like.<br>We assume Yes. | 
| 2. Do we need to lower timeout-rate of different players groups separately?<br>If so, which ones, to which value, and how? | Not exactly, but we assume Yes: we need to take care more thoroughly of the 'decent' ones.<br>We do not influence poor-connection users, but make leaving senseless and waiting shorter and less irritating. | 
| 3. How to distinguish between differents subtypes of timeouts? | On the basis of lanetcy over last 20 matches if Disconnection Categories is implied.<br>On the basis of the timeout-rate if Abandonment Penalty is implied. |
| 4. What is the size of the users population we need to make statistically reasonable conclusions and confirm figures of merits are achieved? | The answer depends on MAU and other numbers needed. |

Numbers needed:

> - Retention-rate (or churn-rate)
> - Product self-repayment
> - Average Revenue Per User
> - DAU, WAU, MAU - (we need need MAU apparently); which user id called "active"?
> - DAU/MAU;
> - ~~percent of users addressing to the app's support~~

### Backlog

1. Make matchmaking more like "stable vs stable" and "poor vs poor".
2. It the match has been lasting for too short (less than 2 minutes), noone wins. ~~Players even get their money back~~. Players' ratings remain unchanged.
3. A player can call in question his technical defeat on one of the latest 10 games if he  
    1. got technival loose in this game with timeout;
    2. has good statistics (hasn't been convicted in abandoning games for 10 games before it), or like;
    3. his club supports such an option.
4. Forced restoration for those with poor connection.
5. Distinguish users with poor connection from leavers and disconnection-abusers (for now we assume it is impossible); reveal detailed traits of leavers (winrate, percent of timeouts, moving average latency over the last 20 games, etc.) in order to stop mixing them up.  
6. Introduce extra-punishment for leavers, more severe as compared with surrenders (for surrender it is nothing at all) - in order to foster surrendering and further reduce the number of leavers.

## 8. Timelines and release planing

### Action points

1. Detect and list all the causes of different technical error from the system's side.
2. Measure the biggest latency during the match.
3. Save statistics on latency for every game (at least latency for the last 20 games).
4. Split up and save overall categorical winrate (technical/koks/mars/oin).
5. Show the players if theit connection is usually poor.
6. etc.

### Design

> [Mockups]():  
> .  

### Architechture

> Some changes suggested:  
> .  

### Back-end

> Back-end to-do list:  
> .  

### Front-end

> Front-end to-do list:  
> .  

## 9. В двух словах

1. **Мы не можем сразу отличить злоумышленников от игроков с плохим качеством соединения**. Каждому игроку иногда позволяется изобразить дисконнект.
2. При частом дисконнекте:
    1. Можно пойти по пути - кто часто заканчивают игру таймаутом по своей вине, получают за это уменьшение времени на пребывание в дисконнекте, пока этот банк не опустится до ~~10~~ 0 секунд.
    2. Можно пойти по второму пути - **жестко делить всех на 'обычных' игроков и 'злоумыленников'** - злоумышленник автоматически проигрывает обычному игроку при дисконнекте. При этом обычный + обычный ждут друг друга, а злоумышленник + злоумышленник играют до первого дисконнекта.
        - **Есть несколько таймаутов, истратив которые игрок начинает при дисконнекте проигрывать**.
        - Можно смотреть на какие-то метрики вроде average latency over last 20 games: if it exseeds 200ms, the player is considered unreliable. 
3. На самом деле оба пути - одно и то же. Дискретный переключатель - это штраф в абсолюте. У нас есть инструмент наказания злоумышленника - авто-проигрыш; осталось решить задачу скоринга, чтобы знать, кому восстанавливать таймауты и с какой скоростью:
    1. У обычных игроков таймауты, например, восстанавливаются по 1 за 3 игры (без тех. проигрышей).
    2. У злоумышленников таймауты вообще не восстанавливаются или восстанавливаются 1 из 10 игр.
4. **На чем построить скоринг**. Это можно делать:
    - За счет стрика игр без таймаутов:
        - ~~похоже, данная тактика недостаточно эффективна~~.
    - За счет соотношения числа технических побед и технических поражений.
        - ~~смотрим только на последние игры, например 50 последних игр, чтобы был шанс реабилитации;~~
        - ~~хочется посмотреть на пропорцию: доля дисконнектов, закончившихся техлузом / доля дисконнектов, закончившихся коксом/марсом/оином/сдачей - но ожидается, что она у всех индивидуальна.~~
        - ~~у косящего под плохое соединение технических поражений всегда будет больше, чем технических побед. Как и у человека с действительно плохим соединением. Тоже не годится.~~
    - За счет соотношения максимального и минимального пингов за игру:
        - измерение минимального пинга за игру (min_game_latency)
        - измерение максимального пинга за игру (max_game_latency)
        - ~~измерение среднего пинга за игру (avg_game_latency)?~~
        - фиксация этих данных по каждой партии.
        - данные значения могут оказаться сильно индивидуальными, но для одного и того же игрока в среднем ожидаются постоянными.
    - Поведение max_game_latency по последним 20 играм:
        - Сам max_game_latency ожидается сильно разным для игр без таймаута и игр с таймаутом. Причем и для игроков с плохой связью, и для злоумышленников.
        - **А вот одинаковый min_game_latency для игр с таймаутом и без таймаута - подозрительная вещь**. Для людей с плохой сетью эта ситуация маловероятна, для злоумыленников - реальна.
        - Соотношение max_game_latency / min_game_latency ожидается разным для игроков с плохой связью и для злоумышленников.
        - Соотношение max_game_latency / min_game_latency ожидается постоянным для игроков с плохой связью.
        - Соотношение max_game_latency / min_game_latency ожидается неравномерным для злоумышленников в разрезе их побед и поражений.

<br>

min_latency (таймауты vs обычные)

| Группа пользователей | Разный       | Одинаковый   |
| -------------------- | ------------ | ------------ |
| С плохой связью      | OK           | Маловероятно |
| Злоумышленники       | Маловероятно | OK           |

<br>

max_latency (таймауты vs обычные)

| Группа пользователей | Разный | Одинаковый              |
| -------------------- | ------ | ----------------------- |
| С плохой связью      | OK     | Маловероятно, объяснимо |
| Злоумышленники       | OK     | Маловероятно, объяснимо |

## Предложения

> ---
> 1. Собрать статистику по пингам в каждой партии для каждого игрока (минимальный, максимальный, средний).
> ---

1. **Посмотреть, постоянна ли min_game_latency для обычных игроков (таймауты + обычные матчи).**
2. **Посмотреть, постоянна ли min_game_latency для ливеров (таймауты + обычные матчи).**
3. Посмотреть, постоянна ли max_game_latency для обычных игроков (таймауты + обычные матчи).
4. Посмотреть, постоянна ли max_game_latency для ливеров (таймауты + обычные матчи).
5. Каково среднее и какова дисперсия max_game_latency обычного игрока в обычных матчах?
6. Каково среднее и какова дисперсия max_game_latency ливера в обычных матчах?
7. Каково среднее и какова дисперсия max_game_latency обычного игрока в таймаутах?
8. Каково среднее и какова дисперсия max_game_latency ливера в таймаутах?
9. Повторить пункты 5-8 для min_game_latency
10. Повторить пункты 5-8 для max_game_latency / min_game_latency.

> ---
> - Построить графики в одних осях для 1-4.
> - Построить гистограммы по 5-8, 9, 10.
> - Пункты 1, 2 - подозреваемые. 
> ---
