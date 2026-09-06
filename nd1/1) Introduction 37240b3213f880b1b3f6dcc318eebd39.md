# 1) Introduction

# Elements of Neuronal Dynamics

- 후시냅스 뉴런의 스파이크 효과는 막전위를 측정하는 내세포 전극으로 측정 가능
- 입력이 없으면, 막전위는 상수 $u_\text{rest}$
    - 활동 전위 도착 후 전위는 변하는데, 변화가 양수면 흥분 전위, 음수면 억제 전위
    - 일단 휴지기 때 막전위는 이미 강한 음수(-65mV)

## Postsynaptic Potentials

![스크린샷 2026-06-01 오후 11.01.52.png](1)%20Introduction/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2026-06-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.01.52.png)

![스크린샷 2026-06-01 오후 11.12.29.png](1)%20Introduction/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2026-06-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.12.29.png)

$$
u_i(t) - u_\text{rest} = \begin{cases} 0 & \text{t < 0} \\ \epsilon_{ij}(t) & \text{t > 0} \end{cases}
$$

## Firing Threshold & Action Potential

$$
u_{i}(t) = \sum \limits_j \sum \limits_f \epsilon_{ij} (t - t_j^{(f)}) + u_\text{rest} \\ t_j^{(f)}: j\text{번 뉴런이 f번째로 발화하는 시간 } \\ \epsilon_{ij}: \text{시냅스 후 전위의 크기}
$$

- 입력되는 신호가 적다면 전체 전위의 변화는 PSP 변화의 합과 동일
    - 짧은 시간 동안 도달하는 전위의 수가 많다면 선형성이 깨져 버림
    - 막전위가 100mV 펄스 형태의 일탈을 발생시킴(위의 그림 C)
        - 휴지 전위로 바로 돌아가진 않고 과분극 형태를 거친 후 돌아감
    - epsp가 20~50개 정도 중첩되야 활동 전위가 발생함
        - 왜 20~50개인가: EPSP의 크기는 1mV 정도이고 임계값은 20~30mV

# Integrate-and-Fire

- 발화 시간은 막전위가 아래부터 올라와 특정 역치 값에 도달하는 순간
    - 역치를 $\vartheta$로 표기
- 즉, $u_i(t)$가 아래부터 $\vartheta$에 도달한다면, 그 순간이 바로 $t_i^{(f)}$
- 활동전위를 이처럼 이벤트로 기술하는 뉴런 모델이 바로 IF
    - 막전위의 변화를 기술하는 선형 미분 방정식
    - 신호 발화를 위한 역치

## Integration of Inputs

![스크린샷 2026-06-01 오후 11.25.49.png](1)%20Introduction/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2026-06-01_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11.25.49.png)

- $u_i$: 뉴런 i의 membrane potential
    - 만약 뉴런에 전류 I(t)를 주입하거나, 시냅스 입력을 받으면 변화
- 세포막은 축전기처럼 작동, 절연체의 불완전성으로 인해 전하가 서서히 나감 → 저항
    - 회로도는 위와 같음
- Kirchoff’s law에 의해 $I(t) = I_R + I_C$, $I_R = u_R / R = (u - u_\text{rest}) / R$
    - $I(t) = \frac{u(t) - u_\text{rest}}{R} + C \frac{du}{dt}$

$$
\tau_m \frac{du}{dt} = - [u(t) - u_\text{rest}] + RI(t) \, (\tau_m = RC)
$$

- 중요한 사실: 뉴런의 입력이 없으므로 I(t)는 t > 0일때 0

$$
\therefore u(t) - u_\text{rest} = \Delta u \exp \left( -\frac{t - t_0}{\tau_m}\right) \, (u(t_0) = u_\text{rest} + \Delta u)
$$

## Pulse Input

![스크린샷 2026-06-03 오전 12.30.25.png](1)%20Introduction/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2026-06-03_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.30.25.png)

$$
u(t) = u_\text{rest} + RI_0 \left[1 - \exp\left(-\frac{t}{\tau_m}\right)\right]
$$

- $0 < t < \Delta$에서 해는 다음과 같다.
    - 입력 전류가 영원히 멈추지 않는다면, $t → \infty$일 때 $u(\infty) = u_\text{rest} + RI_0$에 도달
    - 정상 상태에서 축전기의 전하는 변하지 않으므로 전체 세포막 전압은 $u_\text{rest} + RI_0$

### Example

![스크린샷 2026-06-06 오후 5.14.50.png](1)%20Introduction/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2026-06-06_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_5.14.50.png)

### 짧은 펄스와 디랙 델타

$$
u(\Delta) = u_\text{rest} + RI_0 \left[ 1 - \exp \left(-\frac{\Delta}{\tau_m} \right)\right](\Delta << \tau_m) \\ \text{Taylor Series } \rightarrow \exp(x) = 1 + x + \frac{x^2}{2!} + \cdots\\ \text{first-order: } u(\Delta) = u_\text{rest} + R I_0 \frac{\Delta}{\tau_m} 
$$

- 여기서 총 전하 $q$가 일정하도록, $\int I(t) dt = q$를 상수로 유지 → $I_0 = q / \Delta$
    - $u(\Delta) - u_\text{rest} = q\frac{R}{\tau_m} = \frac{q}{C}$
    - $I(t) = q\delta(t) = \lim \limits_{\Delta → 0} \frac{q}{\Delta}$

$$
\tau_m \frac{du}{dt} = -[u(t) - u_\text{rest}] + R q \delta (t) \\ \therefore u(t) - u_\text{rest} = \frac{qR}{\tau_m} \exp \left( -\frac{t}{\tau_m} \right) \rightarrow \text{Impulse-response function}
$$

## The Threshold for spike firing

- $t^{(f)}: u(t^{(f)}) = 𝜗$로 표기하며, 발화 시간 그 자체
    - 한 번 발화 후 세포막 전위는 $\lim \limits_{\delta → 0} u(t^{(f)} + \delta) = u_r$로 리셋됨
    - $S_i(t) = \sum_f \delta(t - t_i^{(f)})$

## Time-Dependent Input

- 역치가 존재하지 않을 때 시간-의존적인 입력이 존재하는 해는 다음과 같다.

$$
u(t) = u_\text{rest} + \frac{R}{\tau_m} \int_0^\infty \exp \left(-\frac{s}{\tau_m}\right) \,I(t - s) ds
$$

- 헤비사이드 함수 또는 정현파 전류 모두 시간-의존적
- 지금까지 우리의 누설 적분기엔 역치가 존재하지 않았다.
    - 세포막 전위가 역치에 도달 → $u$는 $\vartheta$에서 $u_r$로 리셋
    - 전위의 리셋 → $q_r = C(\vartheta - u_r)$ 만큼의 전하를 제거
        - 발화 순간마다 강력한 음의 펄스 → 전하를 빼앗아가는 것으로 모델링
    - 리셋 전류와 리셋 전류를 포함해서 계산한 값은 다음과 같다.

$$
I_r = -q_r \sum_f \delta (t - t^{(f)}) = -C(\vartheta - u_r) S(t) \rightarrow (I + I_r\text{을 위 식에 대입}) \\ \therefore u(t) = u_\text{rest} + \sum_f (u_r - \vartheta) \exp \left(-\frac{t - t^{(f)}}{\tau_m}\right) + \\  \frac{R}{\tau_m} \int_0^\infty \exp \left( -\frac{s}{\tau_m}\right) I(t - s) ds \\ t^{(f)} = \{t | u(t) = \vartheta\}
$$

## Linear Differential Equation vs. Linear Filter: Two Equivalent Pictures

- LIF 모델은 미분방정식과 리셋 조건의 결합
    - $\tau_m \frac{du}{dt} = -[u(t) - u_\text{rest}] + RI(t)$
    - $\lim \limits_{\delta → 0+} u(t^{(f)} + \delta) = u_r$
        - $t^{(f)} = \{t | u(t) = \vartheta\}$
- 선형 방정식은 적분이 가능하므로 위와 같은 식을 산출

$$
u(t) = \int_0^\infty \eta(s) S(t - s)\, ds + \int_0^\infty \kappa(s) I(t - s) ds + u_\text{rest} \\ \eta(s) = (u_r - \vartheta) \exp \left(-\frac{s}{\tau_m}\right), \, \kappa(s) = \frac{1}{C} \exp \left(-\frac{s}{\tau_m}\right) 
$$

## 1.3.6 Periodic drive and Fourier Transform(다음에)

- 푸리에 변환은 다음과 같음

$$
\hat{f}(\omega) = \int_{-\infty}^\infty f(t) e^{-i\omega t} dt = |\hat{f}(\omega)|e^{i\phi_f(\omega)}
$$

# Limitations of the Leaky Integrate-and-Fire Model

- LIF 모델은 매우 단순화된 모델, 뉴런 동역학의 많은 부분을 무시
    - 전시냅스 뉴런이나 전류 주입으로 발생하는 입력은 후시냅스 뉴런과 별개로 선형 적분됨
    - 이로 인해 이전 스파이크에 대한 기억이 유지되지 않음

## 적응, 버스팅, 그리고 억제성 반동

- $I_1$일 때 휴지기라고 생각하고, t에서 $I_2$로 전환한다고 하자.
    - 간격이 크다면 스파이크를 유발
        - 정상 상태가 도달할 때까지 스파이크 간격이 증가하는 스파이크 열로 나타남
        - regularly-firing neurons
    - 표준 LIF 모델은 스파이크 직후 전압을 항상 동일한 값으로 리셋 → 적분
        - 즉, 가장 최근의 스파이크 너머 기억은 없다
    - **해결책: refractoriness(불응기)에 기여하는 바를 누적**
- 버스팅 뉴런과 말더듬이 뉴런
    - 지속적인 자극에 대해 스파이크 연쇄 → 긴 휴지기에 의해 흐름이 끊김
- 탈억제성 반동
    - 억제가 해제되는 것만으로도 활동 전위가 발생 가능

## Shunting Inhibition and Reversal Potential

- 시냅스 전 뉴런 j → 시냅스 후 뉴런 i로 전송된다고 가정
    - 문제는 전류의 형태와 진폭은 시냅스후 뉴런의 상태에 의존하지 않음
    - $\text{PSC} \propto [u_0 - E_\text{syn}]$: 시냅스후 전류는 세포막 전위와 시냅스의 역전 전위의 차에 비례한다.
        - 즉, 시냅스후 전위의 형태는 순간적인 탈분극 수전에 의존

## Conductance changes after a spike

- 이전 활동 전위와의 상대적 타이밍에도 영향을 줌

## Spatial Structure

- 시냅스후 전위의 형태는 뉴런 i의 마지막 스파이크 이후 경과한 시간인 $t - t^{(f)}$에 의존!
- 실제 뉴런은 나뭇가지(수상돌기) 모양이라 어디서 자극을 받느냐에 따라 세포체에 도달하는 크기가 다르고 가지 자체에서 쾅 터지는 '수상돌기 스파이크'도 유발하지만, LIF는 모양을 무시함.
- 이런 비선형적 상호작용은 무시됨

# So, What can we expect?

- 극도로 단순화되었지만, 시간상에서 정확한 타이밍을 예측하는데 있어선 놀라울 정도로 정확함
    - 진짜 중요하고 훨씬 더 어려운 질문은, 매개변수 최적화 과정에서 사용되지 않은 '새로운' 시간에 의존하는 입력 전류가 주어졌을 때도 이 뉴런 모델이 실제 뉴런의 발화 시간을 예측할 수 있느냐는 점
- 뉴런 모델에 적응(과 불응기)을 추가하면, 예측은 놀라울 정도로 잘 들어맞음