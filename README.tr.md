# mobile-agent-testers

<a href="https://github.com/pierridotite/explore-compile-replay"><img src="assets/ecr-now-building.svg" alt="Next: every bug becomes a free test. Explore-Compile-Replay" width="340" height="54"></a>
<a href="https://www.linkedin.com/in/pierre-raffalli/"><picture><source media="(prefers-color-scheme: dark)" srcset="assets/linkedin-follow-dark.svg"><img src="assets/linkedin-follow-light.svg" alt="Follow Pierre Raffalli on LinkedIn" width="160" height="54"></picture></a>
<a href="https://trendshift.io/repositories/371956?utm_source=trendshift-badge&amp;utm_medium=badge&amp;utm_campaign=badge-trendshift-371956" target="_blank" rel="noopener noreferrer"><img src="https://trendshift.io/api/badge/trendshift/repositories/371956/daily?language=Python" alt="pierridotite%2Fmobile-agent-testers | Trendshift" width="250" height="55"/></a>

<sub>Şu an üzerinde çalıştığım proje: <a href="https://github.com/pierridotite/explore-compile-replay">Explore-Compile-Replay</a>, bir ajan hata bulduğunda izlediği yolu her PR'da model kullanmadan yeniden çalışan bir teste dönüştürüyor. Henüz erken aşamada.</sub>

**20 farklı telefonda aynı anda çalışan 20 yapay zekâ tester, GitHub'ın ücretsiz runner'larında.**

**[Örnekler](docs/examples.tr.md)** · **[Karşılaştırma](docs/compare.md)** · **[SSS](docs/faq.tr.md)** · **[Personalar](personas.json)** · **[Katkıda bulunun](CONTRIBUTING.md)** · **[Sürümler](https://github.com/pierridotite/mobile-agent-testers/releases)**

[English](README.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [Español](README.es.md) · [Português](README.pt-BR.md) · [Tiếng Việt](README.vi.md) · Türkçe

<sub>Bu sayfa İngilizce README'nin çevirisidir ve güncel olmayabilir. Esas sürüm [README.md](README.md) dosyasıdır.</sub>

Test script'i yazmanıza gerek yok. Her tester, GitHub Actions üzerinde kendi iOS
Simulator'ı ya da Android emülatörü bulunan bir Claude Code ajanıdır. Ajan bir kullanıcı
profiline bürünür (en büyük yazı boyutunda İsveççe bir iPhone SE, %200 yazı ölçeğinde bir Pixel 7,
Almanca bir iPad, sağdan sola Arapça…), uygulamanızı ilk kez kullanan biri gibi gezer
(ya da belirttiğiniz özelliği baştan sona dener) ve ekran görüntüleriyle bir hata raporu yazar.
Flutter, React Native, Expo, native Kotlin ve Swift, Kotlin Multiplatform, Capacitor ve .NET MAUI desteklenir.

GitHub runner'ları public repolarda ücretsizdir. Yalnızca model kullanımı için,
Claude aboneliğiniz ya da API anahtarınız üzerinden ödeme yaparsınız: [bu çalıştırmalarda](docs/runs/) telefon başına yaklaşık 0,15–0,55 $.

<p align="center"><a href="assets/localsend-20.mp4"><img src="assets/localsend-20.gif" alt="LocalSend'i aynı anda kullanan 20 yapay zekâ tester'ın gerçek ekran kayıtları: 14 dilde 10 Android emülatörü ve 10 iOS Simulator, küçük bir Pixel'den 13 inç bir iPad'e kadar. Her tester işini bitirdiğinde telefonunda kaç sorun bulduğu görünür. Tıklayınca video açılır." width="100%"></a><br>
<sub>LocalSend çalıştırmasının gerçek ekran kayıtları; bekleme süreleri kırpıldı. <a href="assets/localsend-20.mp4">Videonun tamamı (MP4)</a> · <a href="docs/runs/localsend-20.md">Cihaz cihaz çalıştırma sonuçları</a></sub></p>

[![Tests](https://github.com/pierridotite/mobile-agent-testers/actions/workflows/tests.yml/badge.svg)](https://github.com/pierridotite/mobile-agent-testers/actions/workflows/tests.yml)
[![Stars](https://img.shields.io/github/stars/pierridotite/mobile-agent-testers?style=flat)](https://github.com/pierridotite/mobile-agent-testers/stargazers)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)
![iOS + Android](https://img.shields.io/badge/platforms-iOS%20%2B%20Android-blue)
![Claude Code plugin](https://img.shields.io/badge/Claude%20Code-plugin-orange)
[![Last commit](https://img.shields.io/github/last-commit/pierridotite/mobile-agent-testers)](https://github.com/pierridotite/mobile-agent-testers/commits/main)
[![Discord](https://img.shields.io/badge/Discord-join-5865F2?logo=discord&logoColor=white)](https://discord.gg/WuaCANscr8)

## Neler yapabilir

Her çalıştırma tek bir amaca hizmet eder; amacı [Kendi uygulamanızı test edin](#kendi-uygulamanızı-test-edin) bölümündeki parametrelerle seçersiniz.

- **Yeni bir kullanıcı gibi keşfetme** (varsayılan). Her persona kendi hedefine ulaşmaya çalışır ve karşısına çıkan engelleri numaralı ekran görüntüleriyle raporlar.
- **Tek bir özelliği baştan sona test etme.** Yazdığınız bir brief, her ajanı bir akışın tamamından geçirir: birkaç adımlı bir rezervasyon, geri alma özelliği olan bir editör, iki ekran arasında senkronizasyon gibi. Ajanlar dokunur, uzun basar, kaydırır ve yazı yazar; uygulamayı arka plana atıp geri döner, nelerin kaydedildiğini görmek için uygulamayı yeniden başlatır ya da doğrudan ilgili özellikten başlamak için bir deep link açar. Brief ile yaklaşık 30 eylemlik varsayılan sınırı da artırabilirsiniz. [AnkiDroid için yazılan brief](briefs/ankidroid.md), yeni bir kartın arka yüz alanının klavyenin altında kaldığını ortaya çıkardı.
- **Bir hatayı her telefonda yeniden üretme.** Bir issue ya da adımları verirsiniz; her ajan ekran görüntüleriyle "evet", "hayır" ya da "belirsiz" diye cevap verir ([briefs/reproduce.md](briefs/reproduce.md)).
- **İyileştirme raporu.** Her persona uygulamayı bir kez kullanır; ardından nerede tereddüt ettiğini, ne beklediğini ve öncelikle neyin değişmesi gerektiğini, alana ve etkiye göre sıralayarak anlatır ([briefs/improve.md](briefs/improve.md)).
- **İki sürümü karşılaştırma.** Aynı personalar iki farklı branch ya da build üzerinde çalışır, sonuçlar tek bir tabloda toplanır: ulaşılan hedefler, eylem sayıları, puanlar ve yalnızca bir sürümde görülen sorunlar ([docs/compare-versions.md](docs/compare-versions.md)). Bu, gerçek bir A/B testinin yerini tutmaz; ondan önce yapılacak bir ön kontroldür.
- **Daha ucuz bir model kullanma.** Claude Haiku ya da Anthropic uyumlu herhangi bir API'yi (OpenRouter, DeepSeek, Kimi, GLM, MiniMax, Qwen) kullanabilirsiniz. Bulguların kalitesi, modelin ekran görüntülerini ne kadar iyi okuyup akıl yürütebildiğine bağlıdır ([docs/cheaper-models.md](docs/cheaper-models.md)).

Maestro ya da Appium sizin yazdığınız testleri çalıştırır. Bu ajanlar ise kimsenin test etmeyi düşünmediği şeyleri arar: [Karşılaştırmanın tamamı](docs/compare.md).

## Uygulamalı örnekler

Açık kaynak uygulamalarda yapılmış gerçek çalıştırmalar; hiçbir hata önceden yerleştirilmedi.

| Uygulama | Telefonlar | Bulgular | Süre, model maliyeti |
|---|---|---|---|
| [LocalSend](https://github.com/localsend/localsend) (Flutter, 100 bin yıldız) | 20: 10 Android, 10 iOS, 14 dil | 46 farklı hata, 1 engelleyici hata (blocker): en büyük yazı boyutundaki İsveççe bir iPhone SE'de metin mesajı hiç gönderilemiyor | 69 dk, 4,62 $ |
| [AnkiDroid](https://github.com/ankidroid/Anki-Android) (Kotlin, 12 bin yıldız, release APK) | 10 Android | 43 farklı sorun; bunlar arasında %200 yazı ölçeğinde yarısı kesilen cevap butonları ve üç dilde İngilizce kalmış "Get started" butonu var | 10 dk'dan kısa, 4,69 $ |
| [Flutter'ın animasyon örneği](https://github.com/flutter/packages/tree/main/packages/animations/example) | 1 Android, 1 iOS | İki ajanın birbirinden bağımsız olarak bulduğu aynı yazım hatası ve karanlık modu desteklemeyen bir uygulama | 19 dk, 0,47 $ |

LocalSend'de bulunan 46 hatanın 34'ünün yazı boyutu ya da erişilebilirlikle bir ilgisi yoktu: bozuk akışlar, hata vermeden başarısız olan işlemler, eksik çeviriler ve tablet düzenleri. Ekran görüntüleri, tüm bulgular ve çalıştırmaları tekrarlamak için gereken komutlar: [docs/examples.tr.md](docs/examples.tr.md).

## Hızlı başlangıç

```bash
gh repo create my-testers --public --template pierridotite/mobile-agent-testers --clone
cd my-testers && ./setup.sh           # anahtar çifti + secret'lar + Claude token'ı (Windows: .\setup.ps1)
gh workflow run agent-testers.yml     # demo: 2 Android + 2 iOS tester, ~20 dk
bash scripts/collect.sh <run id>      # raporların şifresini çözer, tekrarları gruplar: runs/<id>/SUMMARY.md
```

Uygulamanızın tüm ekranlarını tek bir haritada, test edenlerin yolları ve her ekranda bir ısı haritasıyla görmek ve her ekrana yorum eklemek için: `python3 scripts/dashboard.py runs/<id>` ([docs/dashboard.md](docs/dashboard.md)). [Demoyu deneyin](https://pierridotite.github.io/mobile-agent-testers/) veya [videoyu izleyin](assets/dashboard-demo.mp4).


Demo uygulamaya [bilerek 11 hata yerleştirildi](demo-app/BUGS.md). [Bir test çalıştırmasında](docs/runs/) 4 demo tester bu hataların 9'unu buldu. Her ajan 2–7 dakika çalıştı; build'ler dahil tüm süreç yaklaşık 21 dakika sürdü. Ajanlar bunların dışında, kimsenin bilerek eklemediği gerçek sorunlar da buldu: Android gezinme çubuğunun altında kalan bir buton ve uygulama yeniden başlatılınca kaybolan veriler. 4 tester'ın toplam model maliyeti 0,87 $ oldu.

Ya da uygulamanız için kurulumu Claude'a bırakabilirsiniz:

```
/plugin marketplace add pierridotite/mobile-agent-testers
/plugin install mobile-agent-testers@mobile-agent-testers
```

## Kendi uygulamanızı test edin

```bash
gh workflow run agent-testers.yml -f source_repo=you/app -f app_id=com.you.app \
  -f android_personas=anna,malik -f ios_personas=clara,jonas
```

Tüm parametreler (build'ler, brief'ler, hata raporları, daha ucuz modeller, build argümanları, video kaydı) ve desteklenen framework'ler: [docs/configuration.tr.md](docs/configuration.tr.md).

## Katkıda bulunun

Yardım beklediğimiz konular aşağıda. Aynı işi iki kişi yapmasın diye, başlamadan önce hangisini üstlendiğinizi bir issue ile bildirin. Her birine nereden başlanacağı ve çevrim dışı nasıl test edileceği [CONTRIBUTING.md](CONTRIBUTING.md) dosyasında anlatılıyor.

- **Diğer ajan CLI'ları**: OpenCode, Codex CLI, Gemini CLI, Goose. Araçlar sade script'lerden, görev de bir Markdown brief'inden oluştuğu için ajanı değiştirmek platform başına tek bir komut demek.
- **Web uygulamaları**: aynı personaları Playwright ile bir mobil tarayıcıda çalıştırmak; PWA'lar ve mobil siteler için.
- **Fiziksel Android telefonlar**: testleri self-hosted bir runner üzerinden, adb ile gerçek telefonlarda çalıştırmak.
- **Yeni personalar**: renk körlüğü filtreleri, yavaş ya da kesintili ağ.
- **Bulgulardan issue'lara**: özeti, ekran görüntüleriyle birlikte taslak GitHub issue'larına ya da bir Slack veya Discord mesajına dönüştürmek.
- **Diğer CI sistemleri**: GitLab CI, Bitrise, Codemagic.
- **Daha fazla build sistemi**: NativeScript, Unity, Godot; her biri `scripts/build/` içinde bir case olarak.
- README ve dokümanlar için **çeviriler**.
- **Model karşılaştırması**: demo uygulamadaki 11 yerleştirilmiş hata küçük bir benchmark işlevi görür. Her modelin hangi hataları bulduğunu ve maliyetini gösteren bir tablo.

## Ekipler için barındırılan sürüm (araştırılıyor)

Buradaki workflow ücretsiz, açık kaynak ve eksiksiz kalmaya devam edecek. Private uygulamaları olan ekipler için barındırılan bir sürüm üzerinde çalışıyorum. Bu sürüm; macOS runner'larını (private bir repoda GitHub her macOS dakikasını on dakika olarak hesaplar) ve raporların ürün yöneticileri dahil tüm ekiple paylaşılabileceği bir web panelini içerecek.

Bu, ekibinizin işine yarar mı? [Üç soruyu cevaplayın](https://github.com/pierridotite/mobile-agent-testers/issues/new?template=teams.yml) ya da [LinkedIn'den bana yazın](https://www.linkedin.com/in/pierre-raffalli/). Kendi uygulamanızda zaten denediniz mi? [Neler bulduğunuzu ve nerede takıldığınızı paylaşın](https://github.com/pierridotite/mobile-agent-testers/issues/new?template=usage-feedback.yml).

## Yıldız geçmişi

[![Star History Chart](https://api.star-history.com/svg?repos=pierridotite/mobile-agent-testers&type=Date)](https://star-history.com/#pierridotite/mobile-agent-testers&Date)

## Teşekkürler

[Claude Code](https://docs.claude.com/en/docs/claude-code) ·
[AXe](https://github.com/cameroncooke/axe) ·
[android-emulator-runner](https://github.com/ReactiveCircus/android-emulator-runner)

## Katkıda bulunanlar

Katkıda bulunan herkese teşekkürler. Siz de yardım etmek ister misiniz? [Buradan başlayın](CONTRIBUTING.md).

<a href="https://github.com/pierridotite/mobile-agent-testers/graphs/contributors"><img src="https://contrib.rocks/image?repo=pierridotite/mobile-agent-testers" alt="Contributors" /></a>

Geliştiren: [@pierridotite](https://github.com/pierridotite) ([LinkedIn](https://www.linkedin.com/in/pierre-raffalli/)) · MIT lisansı
