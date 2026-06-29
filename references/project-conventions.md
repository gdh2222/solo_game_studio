# 프로젝트 컨벤션 (조회용)

UE5 + GAS 로그라이트의 고정 컨벤션. 프로그램/아트/QA 팀이 구체적인 네이밍·구조·진단이 필요할 때만 연다.
SKILL.md 본문에 다 넣으면 부풀기 때문에 여기로 분리했다.

---

## GAS 개발 표준 (프로그램)

- 커스텀 시스템보다 **GAS를 우선**한다.
- **어트리뷰트를 직접 수정하지 않는다.** 변경은 반드시 **GameplayEffect**를 경유한다.
- **GameplayAbility는 가볍게** 유지한다. 무거운 로직을 어빌리티에 박지 않는다.
- 비동기 동작은 **AbilityTask**로 처리한다.
- **게임플레이 로직과 애니메이션을 분리**한다.
- **enum보다 GameplayTag**를 선호한다.
- **서버 권위(server-authoritative)** 게임플레이를 기본으로 한다.

---

## Gameplay Tag 카테고리

태그는 아래 최상위 카테고리 아래에 일관되게 둔다:

```
Ability.*      Cooldown.*    State.*     Status.*    Input.*
Weapon.*       Character.*    Damage.*    Effect.*    UI.*
```

---

## 폴더 구조 & 에셋 프리픽스

```
Content/
  Blueprints/  Characters/  Abilities/  Effects/  Input/
  Animation/   Meshes/      Materials/  UI/       Audio/
  Maps/        Developer/
```

프리픽스:

| 프리픽스 | 의미 |
|---|---|
| `GA_` | GameplayAbility |
| `GE_` | GameplayEffect |
| `GC_` | GameplayCue |
| `AS_` | AttributeSet |
| `ASC_` | AbilitySystemComponent |
| `BP_` | Blueprint |
| `WBP_` | Widget Blueprint |

---

## GAS 어빌리티 디버그 체크리스트 (QA)

어빌리티가 발동/작동하지 않을 때, 추측하지 말고 이 순서로 확인한다:

1. 어빌리티가 **부여(granted)** 되었는가
2. **ASC**(AbilitySystemComponent)가 유효한가
3. **Avatar**가 유효한가
4. **태그가 차단(blocked)** 되고 있지 않은가
5. **쿨다운**이 남아 있지 않은가
6. **코스트**가 충족되는가
7. **GameplayEffect**가 제대로 적용되는가
8. **리플리케이션**이 정상인가
9. **GameplayCue**가 트리거되는가
10. **예측(prediction)** 처리가 맞는가

---

## 아트 가독성 메모

- 공격 애님은 3~6프레임으로 스내피하게. 굼뜬 프레임 수는 손맛을 죽인다.
- 가독성은 색상(hue) 대비보다 **명도(value) 대비**로 잡는다(색맹·난전에서도 읽힘).
- 디테일은 배경이 아니라 플레이어 주변에 몰아준다.
- 스타일 가이드를 정하고 지킨다. 스타일 혼용 금지.
