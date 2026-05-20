# Рекомендации по участию в разработке Shine

Как правило, мы следуем [рекомендациям upstream по созданию PR](https://docs.spacestation14.com/en/general-development/codebase-info/pull-request-guidelines.html) в вопросах качества кода и прочего.

Важно: не делайте веб-редакции. Дословно из документации выше:
> Не используйте веб-редактор GitHub для создания PR. PR, отправленные через веб-редактор, могут быть закрыты без рассмотрения.

Upstream — это репозиторий [space-wizards/space-station-14](https://github.com/space-wizards/space-station-14), на котором работает wizden.

# Контент, специфичный для Shine

В общем случае всё, что вы создаёте с нуля (а не модифицируете существующий код из upstream), должно находиться в подпапке Shine — `_sh`.

# Изменения в upstream-файлах

При модификации файлов, не относящихся к Shine (то есть файлов, которые находятся **не** в папках `_sh`), придерживайтесь нескольких правил, чтобы нам было проще управлять проектом.

Прежде всего, **добавляйте комментарии к новым или изменённым строкам или рядом с ними** в upstream-файлах. Объясняйте, что было изменено, чтобы облегчить разрешение конфликтов слияния; мы регулярно вливаем новые изменения из upstream в наш проект.

### Изменение Upstream YAML (.yml) файлов

**Добавляйте комментарии к изменённым строкам или рядом с ними.**

Если вы добавляете новый компонент к прототипу, добавьте пояснение к строке `type: ...`. Пример:

```yml
- type: entity
  parent: MobSiliconBase
  id: MobSupplyBot
  components:
  - type: InteractionPopup # shine-edit start - Make supplybots pettable # shine-edit end
    interactSuccessString: petting-success-supplybot
    interactFailureString: petting-failure-supplybot
    interactSuccessSound:
      path: /Audio/Ambience/Objects/periodic_beep.ogg
```

Если же вы просто изменяете некоторые поля компонента, комментируйте сами поля, используя строчные или блочные комментарии. Примеры:

```yml
- type: entityTable
  id: FillLockerWarden
  table: !type:AllSelector
    children:
    - id: ClothingHandsGlovesCombat
    - id: ClothingShoesBootsSecurityMagboots # shine-edit start - Added security magboots. # shine-edit end
    - id: ClothingShoesBootsJack
    # shine-edit start - removed for incongruence
    #- id: ClothingOuterCoatWarden
    #- id: ClothingOuterWinterWarden
    # shine-edit end
    - id: RubberStampWarden
    - id: DoorRemoteArmory
    - id: HoloprojectorSecurity
    # shine-edit start
    - id: WeaponEnergyShotgun
    - id: BoxPDAPrisoner
    - id: LunchboxSecurityFilledRandom
      prob: 0.3
    # shine-edit end
```

### Изменение Upstream C# (.cs) файлов

Если вы добавляете много кода на C#, используйте преимущества частичных классов. Разместите новый код в отдельном файле в папке `_sh`, если это целесообразно.

В противном случае **добавляйте комментарии к новым или изменённым строкам или рядом с ними.**

Комментарий к новому импортированному пространству имён:
```cs
using Content.Server.Psionics.Glimmer; // shine-edit
```

Пара комментариев, ограничивающая блок добавленного кода:
```cs
private EntityUid Slice(...)
{
    ...

    _transform.SetLocalRotation(sliceUid, 0);

    // shine-edit start - deep frier stuff
    var slicedEv = new FoodSlicedEvent(user, uid, sliceUid);
    RaiseLocalEvent(uid, ref slicedEv);
    // shine-edit end

    ...
}
```

### Изменение Upstream файлов локализации Fluent (.ftl)

**Перемещайте все изменённые строки локализации в новый файл Shine** — используйте файл `.ftl` в папке `_sh`. Закомментируйте старые строки в upstream-файле и укажите, что они были перемещены.

Пример:

Закомментированная старая строка в `Resources\Locale\en-US\xenoarchaeology\artifact-analyzer.ftl`
```
# shine-edit start - moved to _sh file
#analysis-console-info-effect-value = [font="Monospace" size=11][color=gray]{ $state ->
#    [true] {$info}
#    *[false] Unlock nodes to gain info
#}[/color][/font]
# shine-edit end
```

Новая версия строки в `Resources\Locale\en-US\_sh\xenoarchaeology\artifact-analyzer.ftl`
```
analysis-console-info-effect-value = [font="Monospace" size=11][color=gray]{ $state ->
    [vagueandspecific] {$vagueInfo} ({$specificInfo})
    [vagueonly] {$vagueInfo} (unable to detect details)
    [simple] {$specificInfo}
    [hidden] Unable to detect (unlock to discover)
    *[noinfo] Unlock nodes to gain info
}[/color][/font]
```

Также имейте в виду, что файлы fluent (.ftl) **не поддерживают комментарии на той же строке**, что и значение локализации, поэтому будьте внимательны при комментировании.

### Ранние слияния

Обычно мы сливаем изменения из upstream большими порциями (например, за месяц PR-ов upstream разом), но срочные изменения могут быть слиты раньше, отдельно.

Ранние слияния являются исключением из вышеперечисленных правил — если вы cherry-pick'аете PR для раннего слияния, вам не нужно добавлять комментарии `shine-edit start/end`, так как код приходит напрямую из upstream без каких-либо изменений.

# Маппинг

Если вы хотите внести изменения в карту, свяжитесь с её мейнтейнером, чтобы убедиться, что вы не вносите изменения одновременно.

Конфликты карт делают PR взаимоисключающими, поэтому либо ваша работа, либо работа мейнтейнера будет потеряна. Общайтесь, чтобы избежать этого!

Пожалуйста, составляйте подробный список **всех** изменений (даже незначительных) с указанием локаций при отправке PR. Это помогает проверяющим сосредоточиться на них без необходимости искать отличия по всей карте. Пример: [Правки карты](https://github.com/DeltaV-Station/Delta-v/pull/3165)


**Отправка PR с картой**

Пожалуйста, ограничивайте чейнджлог для PR с картами **значительными** изменениями или дополнениями карты. Незначительные правки карты не требуют чейнджлога.
Формат для PR с картами выглядит так:
```
:cl: ВашеИмя
MAPS:
- add: ИмяКарты: Добавлено веселье!
- remove: ИмяКарты: Убрано веселье!
- tweak: ИмяКарты: Изменено веселье!
- fix: ИмяКарты: Исправлено веселье!
``` 

# Перед отправкой

Перепроверьте ваш дифф на GitHub перед отправкой: ищите непреднамеренные коммиты или изменения и убирайте случайные пробелы или изменения окончаний строк.

Кроме того, для долгоиграющих PR, если вы видите `RobustToolbox` в изменённых файлах, вы должны откатить эти изменения. Используйте `git checkout upstream/master RobustToolbox` (заменив `upstream` на имя вашего удалённого репозитория ss14-art/shine).

# Чейнджлоги

По умолчанию все чейнджлоги попадают в чейнджлог Shine. Вы можете использовать чейнджлог администраторов Shine, указав `SHINEADMIN:` на строке после `:cl:`.

Не используйте `ADMIN:`, так как **это испортит** upstream чейнджлог администраторов!

# Дополнительные ресурсы

Если вы новичок в разработке SS14 в целом, ознакомьтесь с [документацией SS14](https://docs.spacestation14.io/) или попросите помощи в `#contribution-help` в [Discord](https://discord.gg/qcK4ZKFNUb)!

## Контент, сгенерированный ИИ
Код, спрайты и любой другой контент, сгенерированный ИИ, **не запрещён**, однако он должен проверяться более тщательно и быть помечен лейблом `AI`.
