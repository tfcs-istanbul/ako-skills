# ako-skills

[ako-starter](https://www.npmjs.com/package/create-ako-app) ve [mari-ui](https://github.com/tfcs-istanbul/mari-ui) ile proje üretmek için AI ajan skill'leri.

| Skill | Ne yapar |
| ----- | -------- |
| `/ako-starter` | Proje fikrini dinler, ihtiyaç analizini çıkarır (`PROJE-ANALIZI.md`), onayla `create-ako-app` ile kurar ve ilk aşamayı iskeletler. |

## Kurulum (Claude Code)

Kişisel (tüm projelerde):

```bash
git clone https://github.com/tfcs-istanbul/ako-skills.git ~/ako-skills && ln -s ~/ako-skills/skills/ako-starter ~/.claude/skills/ako-starter
```

Yalnızca bir projede: `skills/ako-starter` klasörünü projenin `.claude/skills/` altına kopyalayın.

## Kullanım

```text
/ako-starter Kafeler için sadakat kartı uygulaması: müşteri mobilde QR okutur, 10 kahvede 1 bedava...
```

Skill önce eksikleri sorar, sonra planı yazar, onayınızdan sonra kurar. Her aşamada durup onay ister.
