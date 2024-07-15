
<!-- rnb-text-begin -->

---
title: "Top International Goal Scorers in Men's Soccer: Pull from Wikipedia"
output: html_notebook
---

# Setup 


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeSh0aWR5dmVyc2UpXG5saWJyYXJ5KGphbml0b3IpXG5gYGAifQ== -->

```r
library(tidyverse)
library(janitor)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5BdHRhY2hpbmcgcGFja2FnZTog4oCYamFuaXRvcuKAmVxuXG5UaGUgZm9sbG93aW5nIG9iamVjdHMgYXJlIG1hc2tlZCBmcm9tIOKAmHBhY2thZ2U6c3RhdHPigJk6XG5cbiAgICBjaGlzcS50ZXN0LCBmaXNoZXIudGVzdFxuIn0= -->

```

Attaching package: ‘janitor’

The following objects are masked from ‘package:stats’:

    chisq.test, fisher.test
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShzY2FsZXMpXG5saWJyYXJ5KGdndGV4dClcbmxpYnJhcnkoaHRtbHRvb2xzKVxubGlicmFyeShzeXNmb250cylcbmxpYnJhcnkoc2hvd3RleHQpXG5saWJyYXJ5KHJ2ZXN0KVxuYGBgIn0= -->

```r
library(scales)
library(ggtext)
library(htmltools)
library(sysfonts)
library(showtext)
library(rvest)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5BdHRhY2hpbmcgcGFja2FnZTog4oCYcnZlc3TigJlcblxuVGhlIGZvbGxvd2luZyBvYmplY3QgaXMgbWFza2VkIGZyb20g4oCYcGFja2FnZTpyZWFkcuKAmTpcblxuICAgIGd1ZXNzX2VuY29kaW5nXG4ifQ== -->

```

Attaching package: ‘rvest’

The following object is masked from ‘package:readr’:

    guess_encoding
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShndClcbmxpYnJhcnkoc3lzZm9udHMpXG5saWJyYXJ5KHNob3d0ZXh0KVxubGlicmFyeShjb3VudHJ5Y29kZSlcbmBgYCJ9 -->

```r
library(gt)
library(sysfonts)
library(showtext)
library(countrycode)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBGaXJzdCBhcmd1bWVudCA9IG5hbWUgaW4gUlxuIyBTZWNvbmQgYXJndW1lbnQgPSBwYXRoIHRvIC5vdGYtZmlsZVxuZm9udF9hZGQoJ2ZhLXJlZycsICdmb250cy9Gb250IEF3ZXNvbWUgNiBGcmVlLVJlZ3VsYXItNDAwLm90ZicpXG5mb250X2FkZCgnZmEtYnJhbmRzJywgJ2ZvbnRzL0ZvbnQgQXdlc29tZSA2IEJyYW5kcy1SZWd1bGFyLTQwMC5vdGYnKVxuZm9udF9hZGQoJ2ZhLXNvbGlkJywgJ2ZvbnRzL0ZvbnQgQXdlc29tZSA2IEZyZWUtU29saWQtOTAwLm90ZicpXG5gYGAifQ== -->

```r
# First argument = name in R
# Second argument = path to .otf-file
font_add('fa-reg', 'fonts/Font Awesome 6 Free-Regular-400.otf')
font_add('fa-brands', 'fonts/Font Awesome 6 Brands-Regular-400.otf')
font_add('fa-solid', 'fonts/Font Awesome 6 Free-Solid-900.otf')
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuc3lzZm9udHM6OmZvbnRfYWRkX2dvb2dsZShcIkJhcmxvd1wiLFwiYmFybG93XCIpXG5zaG93dGV4dDo6c2hvd3RleHRfYXV0bygpXG5zaG93dGV4dDo6c2hvd3RleHRfb3B0cyhkcGk9MzAwKVxuYGBgIn0= -->

```r
sysfonts::font_add_google("Barlow","barlow")
showtext::showtext_auto()
showtext::showtext_opts(dpi=300)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZmxhZ19kYiA8LSByZWFkLmNzdihcIkNvdW50cnlfRmxhZ3MuY3N2XCIpICU+JSBcbiAgI0NvbnZlcnQgY291bnRyeSBuYW1lcyBpbnRvIDMtbGV0dGVyIGNvdW50cnkgY29kZXNcbiAgbXV0YXRlKENvZGUgPSBjb3VudHJ5Y29kZShzb3VyY2V2YXIgPSBDb3VudHJ5LCBvcmlnaW4gPSBcImNvdW50cnkubmFtZVwiLCBkZXN0aW5hdGlvbiA9IFwiaXNvM2NcIiwgd2FybiA9IEZBTFNFKSkgJT4lIFxuICBzZWxlY3QoQ291bnRyeSwgZmxhZ19VUkwgPSBJbWFnZVVSTClcbmBgYCJ9 -->

```r
flag_db <- read.csv("Country_Flags.csv") %>% 
  #Convert country names into 3-letter country codes
  mutate(Code = countrycode(sourcevar = Country, origin = "country.name", destination = "iso3c", warn = FALSE)) %>% 
  select(Country, flag_URL = ImageURL)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


# Scrape Wikipedia Data 


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudXJsX2dvYWxzIDwtICdodHRwczovL2VuLndpa2lwZWRpYS5vcmcvd2lraS9MaXN0X29mX21lbiUyN3NfZm9vdGJhbGxlcnNfd2l0aF81MF9vcl9tb3JlX2ludGVybmF0aW9uYWxfZ29hbHMnXG5gYGAifQ== -->

```r
url_goals <- 'https://en.wikipedia.org/wiki/List_of_men%27s_footballers_with_50_or_more_international_goals'
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibnJvdyI6ODAsIm5jb2wiOjExLCJzdW1tYXJ5Ijp7IkEgdGliYmxlIjpbIjgwIMOXIDExIl19fSwicmRmIjoiSDRzSUFBQUFBQUFBQTlWY3oyL2NWbjZmeEZaa1M3SXNKOEdpUllHVWJlSHU3c0dlSWVjWFdUU1FaY242TFZ2UnlFNGN4WkhmREo5bUdISElDWDlJa1hyeFpkSGpIbnBxRDBXRDl0SWVGZ3UwaHowRWhWRjEvNEcyd0xiYmR1dGt0NXUyS1ZyMHNIdGM5MHZ5ZlIrL3BHWnNqU1VEclFENmtZL3ZmYjZmNzg5SFBnNjhNZmRlZWV5OXNVS2hjSzV3L2p6OE93S25oWkc3bS9QWDlFTGgvS3R3OFVyaGZPRmkxSDRDdDkrQWszRTRwdUJZRnpjV08wSFE4MytyV0F4N3Rzdk02L3ZXcnRYbHBzV3V1MTY3R0YzMW9xdGl5KzEyWGNjdlZvdlZWbkhlWnUxdGQyZDczZldDc00zczYvNWVXK0F0RFltbkZsVW04V2E4Tm5jQ3kyRUVjRzVJd0ZheGxRSXVlY3doV0RkT2lNV2RZcVZZVVZNWUp4cVQ0Z3hydEZxeFZwTmdhOHhtQjM0Rzc3M2hkV3hLdktERHQrODZWc0JOc0I5cmJ0L3FXaDRMdUUvd0cwUGlHMFZEay9nM3VkMjJ3dTcyVlUxdldYdVdmVlV6Q1BUQzhOUlR1eTZHVHB0NUJ3UnU1dVFlZ3NqUlNDVGF6REVKMFB5UXZFckZVdXFpOTFtM21YSFFFTFFBcUpyYXptT0hsbjJLYU40cDd0Um9OSDk4dHFRS2hZdFA0ZS9sK0hLSWJJT0E0eEpwbWZVeVdUdXNLMW1ScFJWZ0pkeG5Wa0RRVm9jUERGT2lOVmhvV25HYVpjSmpXSVptMFZRejlXRGZPa1YxQVgwTmliYlpZVll1Rlc2ZTNBL05Zak0xM1FMM3VzdzVlSW5NaGwwc0lFeDJhRkYySFo0dHBNTVdPaWpNbFpTZ1p6bVd5Y3h0SUxtOTZUWloyeVhRdDRiUDNEU2tiN1VQZXNFcHFtWUc3SzRYdGtOMjBDZUJoN1VuTC9KME1WOElZZFhvUWpCbWdMTUNOay9EZS9icWJQbnF6VXJBdDgyclduMXB6N1U4VG14eWIwaHNpTlUwR0c2NnZtT3gySE9MM0R2a2JYY3YreGh4MXFGN3RrWHAvL3Y2QWs5TGFTQTE5cm5KbmY5cjYwdHEvVWFQV2FkWlg4Qm1hZUExdUpkZEM0WU5OUERuRGwwTFRHc3Y4K3kyTWp4ZUdyZ05Od3c2Mnl1dXg5bkxxRDR2b1RJT2F6NjlxS2RQZ1l1dVk0WWU4MThzaUNIY3loSnFIdDRjV3Z3Rm5oc0FDSEk5WFZYSTQza2p5RDJYbjJXMnZneCtaLzR5TjZ4M29hNmt5VEhMdXR4ejNaZjNhSGhtVmZpc25udzNUdnRlT0h2SVc1M3REZDRMbTdiVmVwbFBYc01DZ21mMXRFeFpVTnQ3cm5nY3lDNGF3MVlYZUtSTFBmTU9DNWgzNXBzSnAxdlZ3SlRwV2puSG5TN3pkZ25GTzhQREdSbWZyM2NzMityMUxDZVR5aSt3eUtVczEvZ25Wc3M5eFFyeUhKMWY5djdIR1Q5NERBdW5GYlVVN3A3RkE0ZDFUN0YrUXBWTlBiN1FZYzVwWGtYaEtacThBWVhlTG4vQjdaaG5yNTdENmxndjF0UHlNQXNSemM4OGk4OGVhOWpVaGJnb1pjTDROb2QvdmVoTjR5VS9BZDRmL2lrcmRjZE02QWNlcytGMUs5b1NkSjA5N2tIeVpiY0Z6Mm9GUEx1ZDFrTGhVcnp0SGUySkZ3cXZ4cHZtQlpCU0tFUzc1cStKNDBKVTNPRVlFOGVFbURlWk8xNkg0dzF5ZkkwY3Z5eU9YeUhIVzNEOHFqaCtEWTVmaCtNM3lQR2JjSHhkSE4vTUhkY0dIR1Z5MUFZY3Z3M0gyK0tZN25QTURUaVduM0ZNRmRMUEIxZG1QY3NQTE9hNHlvYnJ3TnVMSzI1TXJGcndqR0FyYTl6M0xkRjNZY2EybERuRzhmcFNJM1FzVzVudGRIamdZZWZrbXJ2YmdWVWJCbmFZN0oySXBxNng1bTRINGhtbmI3aGRib2ZLYXJqTGRzTkM0VkU4Zlo1NzNHa3A2NkcvZS9TcEw0YSt2dUUySVVxVlZiNFB5ZVh1KzdzSWZIbkJOWGM4ZmdBc3JJRFpvZWgrN1RZL2dFVUtKUzJHdnM4dFIya3d6azBoYVdTZDIwZC9pakQzckQyd2d2S3U2NXI3ek1NeGs0MmpUMEdlcDZ5NExkK1NiRlpBYjc5anRibXl3cnFzNndab3RjczNtUTlhS3pOTk03UnQxcEUyWVI5eE05ODdzV0k1RHVzb3NPQkxPNzIrWXJIQThzTmRwY0ZobFFtWjA1WVlsdWY2TnR0VFZtelg1eWh3M1RxQUp5K25EUWJqMTF4SGRJL0hvb0NkYWFFTnhob0I5eHhsMmUwNDBpcXU3N091c3NpZ2NZVEdFNnVoNVN1TjhPaFRqeDlpM3dMM1RHWHQ2RFBiNWdnM1Bzczg0S0ZzaE5ZaDZnTk9hbHBnRTg0YzVEZTJ5RHp2QUlqSW5rdHpsbWx4Q0EvUGJUZVprREIreXdUdnpIMy9ML211Tk9VbTUvQXFDUEUxQjBZd21laWVXbVkrN3lvejlyWEY2UEhmUk1PTlpzTjNmS1lEWlViWllHYkhFakxlZU4rR3AwbEhXV3A2ckdOMTNUM3JyMzhYclo2WUsxcUxJVW90cDhNd1JpZVh1aDVYR3EwTzZPcW55cyt4UGN0VTdsbmdUWUgrNW96TmQ4R01KbmgvelFvOENqOFdCZitNMzlsaEgwdnJkWmh5TSt4ZTJ3M1JHNU9SQ1h6WFVXYlpIdEJBYTYyNUhSWnAwbUJSNENTeUxnbmJyN085b3orWDgrL1lFTUpnMkFXSWs5REUrYk8yNVFUS0hPLzJmSDZBUSsrN1VRQkRQbmE2NmRESjFTaTF3QXV1NHdJRExCQUxyT2xaVUFodVJuRVpoQUU2WXFJQjRRbjl0d0wzNnlUOFRXQUF6bG1EZ2Z0b213dVE2QkJQbGh5MndnN0RBeGN5Q0V3RjcvdG9wbVh3em9wTGdteGl5ZCtIRUZhV1RFOG0zL2c4MEFSemRyb01tVjllZGxrTFhLbzBBbzliclU1cTlxN0xENEZPV3JBZ3RhUDBQQVM5VWNPSmQ5bUJ3Nkg4UWIxREMwMnN1eEFQdDBGdm4wdExSQS9tU21TNmRpZjBtOEJDcUhkbG1jV0dYNFQ4aXNvRng0UzRzaHlaazNWc1pkUHRRcExKOUp5YU1SM1FkUVp1TVBzZzlmYjRLdnNJL0xvSk9oeGdCVm85K2pObDl1Z3ZJTVB2UVdES2NncUo2MEx0V0RpUW1UdTV5SFlCOVB0L2VQVFo3dEZuc3ZSdGRvQWJwT0FpZHp3RXZRekIra21VNWtDMzFaRjhKOVo0QjB5N3lUemVsU1piZ1NMZUJlKzM0Y2tHTzZjZzB5RmZJVXFVZGU3NUZ1YjI1Q0tVNXpaVUQrZGF4NVdWYTJ3VEFHWWg1MndieHpVNmx2T1JwZHpaWllkTWx2STMzMmNXNURDVVNTdXFCbGlXTXV2VkJmeGtMYTR2eWwwSzBYRStlcVlUNXlQeGQxK2NpVThUS0MxNTUxQ2lkdzRGM3ptd21JaHZwbmdwWGlGd2JVaytWdUpWOHJFUnI1SzlCRUxtNDc1M2Z1bVcwNDVBRkd4aEhRbDQ2UG45Ulk3RXoxV0lsR3g4cEhrWVJ2a1FmOVBDRWNrM0tkUWN0NzhSVzN3WUduRDdvdHdlRUIxdjRJY1ZKU0thZkZoQlh2SDJIK0tLclVXWlY5d1BsS3lzaS9JakJXTGozb2JpN2loTEhxYzBoV2t3TjViMlhBampXWmY1S1BCcnlWZURtQmI1YWpCQXI2elpudUdvWlA4YmEwc2NOa3pKUlUvZVAvR2V0QVNJOTVSSjNNVjd3cWhIL0VTdnhFLzAvUTJYTWVvRjNCTkY4T1RWRExOVEJIR3k4OWRIbWI0RGppWE5CZHlhTzRHcE1xRTRHVzlRS2VqRVFSRjBVVzRRWVd6Y1lzZGlZeVRlN09tVHhybEFHQlg3RDJoUHNsOGl3ei9lNytnLy9wbDVuL1hxcUhqWFI0THh1enJLU042MSszcGxKSDdoN2FNSlBSOG5MNHVEUStPaWZGbnJaLzYwcG1XcjVQbTd0K1pucEcvdjNGNjdkZlBPcXJnK056TS9lOUpUaWpQby9OenN6UHp6UmVWdkRVUjdMcnRVM0FDaS9lZEZCR1pueU9UQnRQUFdvOU5PWUlXVGNSbGdwd0dUVCtTSWs4bks2ajFJdDJQbUdtekpaMGc0bGM0dlBHTEE2R2VwZXdKWno0K0JrMlhhQVB3Sk9GV0t5cDM1MmEzT2d3RUF5ZGJGK28ySE53clIzNDB0YkF0SisrNmpwTDBuK3UvbVd6RnU4M0hTTnZLdG1OOFE0emNlUDZjVmVPODhIdEErR3REZXlMV0YvdTI2R0w5K0k5ZUsrM2ZFL1R1Ri91MXRjWDh0M3hhZTNhNCtHckl0OUc5WEhnM1ppbm5MajNKdDRXVHQwcU1oMjhJTHRRV013NDhFVHZ0aDBqYkZkZk5KMHJMSFNmdUJhQitJRnVPekpYQzNSUDlEY2MyVXBIMFg5Uk80R0JjTjBUNUUzQnZaRnZzUjUzNU9EdkxaVWJJOE1XNGUvcEhRUStDOUorUy9uOE5IdnBoUE9PNURNZTVENVAwNHl4L0hZYjdpTlN0a1crUjkvMFpXSDRiOHhMeVd1TWI4ZlNEYURzb1hMZHI5SHZLOWtjVy9MOFo5a05QclEzRTlLMXFzTjFoL2NMd3ArRzNrNXVmSGZTajZUZEhlemJYSTR6N09GL013Zmg0bWNnb2lEcWQvL0syM3Z2Zk9WOSthL3VMYkgzempaMy8xN2VrdjQrYUQ2Ui8vWU96dDNoLy9ZUG9uOGVVM3A3Lzh6cHVIbnk5OFovcW4wZWkzdmpmOVgvSGxtOU9mLzM3MDl3ZXlIK2Q5RWYwNzl2YjBmMFNqRGorZi9ybTQvejlpL0g4THZNK2ozbmYrVTg1RFBrOGlzZC80K2ZTVENLWDNKOU0vM1luL0pCOGM5L2RpM0w4STNvai9KQmEzTWYwandmTmZZem9mU3prNC9rbGlqT2wvRStNUkgrZGorNVdROXhYeUxNZC9xYjVDejM4VTQ3QkZPNkNlUHhUai9rSHdSUDRKek5qMGw2SkYzbjhqL1BMdjhiVEYxRTVDdnNRWDk3SDlrYkQzVDJLWTM1bitKNkhYendRUHZJL3RQd3Y3L0owWUwvMHA5RUErT082SFF1N2Y1dnlOTGRvWFd6bFA2Qy8wTHVERGQ3SzVNcXFWU3VVdkh2MGV1YXltbCtPcVlVUjNvYmVHWFdLRVZ0SXE2YWk2QmwycW9WY0pqcEdCVlVzWjJFbzFubERUeUFROU02S21KNUNsZ1JqMWVqekNLS1ZkMWFTcnJxWmRzWHFxb1JLMmxRUzZXaVBTS3NuRU90RzhsbWhlUHk2UmFwN0E2K3B4azlXSnlkUzRpNUxRMVFTTHdOY0VlNE5nSmJaV05US3htdlZJWkxwNjFuUzFCSWRJTS9RRXB6YTRLekl3OVQzQWFsbldPVW5IQlJ2SmhGS1pkRlVTREdJZlhjdHBMdTJqa1luVlJJa2FZVnhLdWpRNlVkaW5UcFRJeFhNNUd6UWlVbWs4SjRiUVNDeXFhcjhrVUV2cEpGWE5KUUhnQ0ZYMTR4YWswa3JIUXNGSXNFckV5VVk5TjBvb1FtaEdsa3hHbGFwa1lnSmZJa2xoR0VrWENhdDhja1dHTVk3SFk5S2xWd1lhVjYxa0E2YWNzd0RrWFNueFdaV01TaEpMTlVpWGtldEtMVUFvNnVWakZLdlZYTUtuYnFnZDUwWGh0V1BablpjNEtxZ095SSsrWVpHUHg0aTFudk51LzBqUmoxSFVTMUxkekliSmhGWlRsa09ISzNGOGlLMHp6VkRXbU5mcUtMSG1Zc1BMVUphWkV6THZRSWtqSXVtZEtxdktIRy94YnBONzBlZ3FqdFkwWlNac2gzNmdnRUVsQm93V3ZURzdwUGV5V2xMdXRBSlhRQmlTV1FXWTJRY0FVTlVRb0VwSDFoR2dydHgyOXhJT0lFMUhicXFhOWhOTkxxbDFvVjRjam1JSFNncXJWUW5iTlJaMWxZd3RFMTlOcjZpRzB1QzlBTVZWRVdGQzFSR2lqbnludENvMVQwbVRGS3JLVE0rejdBeUZtcHlQS2x6V3l0VHFxalJOWFRvTlBYRzVYSkpEQVJTdGVFa25mdEFrMVRMT0wxVUkxWG5lOUFTQW9jdGdLS2ZCb0dkMEJRQUNPaG5wSkoyclVic21USkg5dUNTdmFUSUVxSjV5OGlWTlQyWFhwVnNyMUtZYXdsNEJBNlNPb1RFS0hpTnhBQXNLRWlhMk1hVExLaGtVbVJSVEtuRWxSSW5VcG95V1NPTVJBbytFcVNRSVhxUFFXcXBtbjN5YnFtYkNySjZxcjJlaVdqb2EwZ1ZCdEhJZkE1WU02V21OSWtnYXFWOGtpWWxxU2t5R2FUVUowNmgreTNnMFpEeWxsU0ZyUjNWQXY4dzJuZGdzUmFsbnJHQklLK2haWDlmNytUcGp0UnIxbmxHVnpHWFM2V1hKTUZQVHBERXZRK0NsUWFwVitsT1JDazJvRll3TXJTcjlvZlZKSmsxbW8reWIwaksxYTVCK2hxeHBXbHBRYW1sS2wvb1d3QW1JVHhUWVAyWkxNZ3FOckoyTjU4WHl1RnhPcElHeUswZGE5Y3MwU2RCQ2FiMG9wY1doMUsvcTl5ME9sK0thbmRUMlkydmQ2SmIyWUt1c1l5VS92MVUyOEh4aVM2cysyS3FVNEZEVCs1VktlbC9WNFY0eUpyMWZJK2YxOUZ5bEdFUmV4VWpQcXdTblNzYVhxM2grWVV1dFA5aXFhdWs5amM2dmtQTXFPU2VjeXVTOFN2aFZDYWNxd2F3UlR1VjZ5cU9tUHRpcUVSNjFNamtuUEdxRVI0M0lyaEhaTlNLN1JtVFhpZXc2c1VlZHlLMFR1WFVpdHk3bG50dWlrSVJDblZDb0V3cDFNbDRuRkhSQ1FTY1VkRUpCSnhSMG9ycE81T3BFcnE2bk5Na1FnNGd5aUNpRGlES0lLSU9JTWlUT2hTMERvc1VncWhsU3RaRXR0VVIwVXpWNlE2VVhtVHRsZWxHaEYxVjZVYU1YZFhxaDB3dktScFZzeHVBQ29rdk5jRktwWkpWS1ZxbGtyVVF2cUI0YW9HWC9HNEVSaDNXNUx3ckNPTnBzSi9xOTVkME4rZjNMWXc1K0xYMnRaN01EK1h1YzF4d1dXUElyOGFXVzYreHdrM3UwYzZUdE1sdCtpVzZ4SHA1UHhqZDYzTnZ1c2tEK1JtZTh4VHdPZlg3NlVmT0t5UUllL2Z5eldnbzYyOUVzREJlUDcrVDB1ZWk1KzlkUnAraDNucTgrZ24rZVBuMzYzYnppTFp2NXFEaDJqb0VrZG4zSGcvbHc5WXZjbEZHM0Yra0ZrMTZOZmlFNm1wdjhpcGZyR1BkYkh1dng3ZWhIcllYazE2ZXZpSU1PTzlkejJ1UjJRUkNQenRmSitYakM1dFduWXZvb3VvQTdiVXYrbUc3RVprMk85aG0xbkpZZG1uanZuTW4zMFBaZ3B0aEsxMkZ4ZFBDNy9oajArdGNETjVBV0htdTVOdmJFQmluODRuOEJIQ01QcjZSQ0FBQT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["flag_URL"],"name":[1],"type":["chr"],"align":["left"]},{"label":["rank"],"name":[2],"type":["int"],"align":["right"]},{"label":["player"],"name":[3],"type":["chr"],"align":["left"]},{"label":["nation"],"name":[4],"type":["chr"],"align":["left"]},{"label":["confederation"],"name":[5],"type":["chr"],"align":["left"]},{"label":["goals"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["caps"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["goalsper_match"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["career_span"],"name":[9],"type":["chr"],"align":["left"]},{"label":["date_of_50th_goal"],"name":[10],"type":["chr"],"align":["left"]},{"label":["ref"],"name":[11],"type":["chr"],"align":["left"]}],"data":[{"1":"https://upload.wikimedia.org/wikipedia/commons/5/5c/Flag_of_Portugal.svg","2":"1","3":"Cristiano Ronaldo","4":"Portugal","5":"UEFA","6":"130","7":"212","8":"0.61","9":"2003–","10":"26 June 2014","11":"[2][38]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg","2":"2","3":"Lionel Messi","4":"Argentina","5":"CONMEBOL","6":"109","7":"187","8":"0.58","9":"2005–","10":"29 March 2016","11":"[39]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"3","3":"Ali Daei","4":"Iran","5":"AFC","6":"108","7":"148","8":"0.73","9":"1993–2006","10":"9 January 2000","11":"[25][40][41]"},{"1":"https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg","2":"4","3":"Sunil Chhetri","4":"India","5":"AFC","6":"94","7":"151","8":"0.62","9":"2005–2024","10":"31 December 2015","11":"[44]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg","2":"5","3":"Mokhtar Dahari","4":"Malaysia","5":"AFC","6":"89","7":"142","8":"0.63","9":"1972–1985","10":"22 August 1976","11":"[18][45][40]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg","2":"6","3":"Ali Mabkhout","4":"United Arab Emirates","5":"AFC","6":"85","7":"115","8":"0.74","9":"2009–","10":"31 August 2019","11":"[46]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/92/Flag_of_Belgium_%28civil%29.svg","2":"6","3":"Romelu Lukaku","4":"Belgium","5":"UEFA","6":"85","7":"119","8":"0.71","9":"2010–","10":"10 October 2019","11":"[47]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"8","3":"Ferenc Puskás","4":"Hungary","5":"UEFA","6":"84","7":"89","8":"0.94","9":"1945–1962","10":"24 July 1952","11":"[11]"},{"1":"https://upload.wikimedia.org/wikipedia/en/1/12/Flag_of_Poland.svg","2":"9","3":"Robert Lewandowski","4":"Poland","5":"UEFA","6":"83","7":"152","8":"0.55","9":"2008–","10":"5 October 2017","11":"[48]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/06/Flag_of_Zambia.svg","2":"10","3":"Godfrey Chitalu","4":"Zambia","5":"CAF","6":"79","7":"111","8":"0.71","9":"1968–1980","10":"7 November 1978","11":"[49]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"10","3":"Neymar","4":"Brazil","5":"CONMEBOL","6":"79","7":"128","8":"0.62","9":"2010–","10":"11 November 2016","11":"[50]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg","2":"12","3":"Hussein Saeed","4":"Iraq","5":"AFC","6":"78","7":"137","8":"0.57","9":"1977–1990","10":"17 March 1984","11":"[51]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"13","3":"Pelé","4":"Brazil","5":"CONMEBOL","6":"77","7":"92","8":"0.84","9":"1957–1971","10":"4 July 1965","11":"[35]"},{"1":"NA","2":"14","3":"Vivian Woodward","4":"England England amateurs","5":"UEFA","6":"75","7":"53","8":"1.42","9":"1903–1914","10":"31 May 1909[d]","11":"[17][52]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"14","3":"Sándor Kocsis","4":"Hungary","5":"UEFA","6":"75","7":"68","8":"1.10","9":"1948–1956","10":"19 September 1954","11":"[29]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9e/Flag_of_Japan.svg","2":"14","3":"Kunishige Kamamoto","4":"Japan","5":"AFC","6":"75","7":"76","8":"0.99","9":"1964–1977","10":"18 July 1972","11":"[54]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/aa/Flag_of_Kuwait.svg","2":"14","3":"Bashar Abdullah","4":"Kuwait","5":"AFC","6":"75","7":"134","8":"0.56","9":"1996–2007","10":"25 December 2002","11":"[55]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/0d/Flag_of_Saudi_Arabia.svg","2":"18","3":"Majed Abdullah","4":"Saudi Arabia","5":"AFC","6":"72","7":"117","8":"0.62","9":"1977–1994","10":"15 April 1984","11":"[56]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/d/d1/Flag_of_Malawi.svg","2":"19","3":"Kinnah Phiri","4":"Malawi","5":"CAF","6":"71","7":"117","8":"0.61","9":"1973–1981","10":"6 July 1978","11":"[36]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/a9/Flag_of_Thailand.svg","2":"19","3":"Kiatisuk Senamuang","4":"Thailand","5":"AFC","6":"71","7":"134","8":"0.53","9":"1993–2007","10":"23 January 2001","11":"[57]"},{"1":"https://upload.wikimedia.org/wikipedia/en/b/ba/Flag_of_Germany.svg","2":"19","3":"Miroslav Klose","4":"Germany","5":"UEFA","6":"71","7":"137","8":"0.52","9":"2001–2014","10":"27 June 2010","11":"[58]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/a9/Flag_of_Thailand.svg","2":"22","3":"Piyapong Pue-on","4":"Thailand","5":"AFC","6":"70","7":"100","8":"0.70","9":"1981–1997","10":"30 January 1989","11":"[59]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9f/Flag_of_Indonesia.svg","2":"22","3":"Abdul Kadir","4":"Indonesia","5":"AFC","6":"70","7":"111","8":"0.63","9":"1967–1979","10":"8 August 1972","11":"[60]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/64/Flag_of_Trinidad_and_Tobago.svg","2":"22","3":"Stern John","4":"Trinidad and Tobago","5":"CONCACAF","6":"70","7":"115","8":"0.61","9":"1995–2012","10":"13 June 2004","11":"[37]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg","2":"25","3":"Hossam Hassan","4":"Egypt","5":"CAF","6":"69","7":"177","8":"0.39","9":"1985–2006","10":"25 February 1998","11":"[61][62]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Uruguay.svg","2":"25","3":"Luis Suárez","4":"Uruguay","5":"CONMEBOL","6":"69","7":"142","8":"0.49","9":"2007–","10":"23 March 2018","11":"[63]"},{"1":"NA","2":"27","3":"Gerd Müller","4":"West Germany","5":"UEFA","6":"68","7":"62","8":"1.10","9":"1966–1974","10":"18 June 1972","11":"[64]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/e/ec/Flag_of_Guatemala.svg","2":"27","3":"Carlos Ruiz","4":"Guatemala","5":"CONCACAF","6":"68","7":"133","8":"0.51","9":"1998–2016","10":"15 August 2012","11":"[65]"},{"1":"NA","2":"27","3":"Robbie Keane","4":"Republic of Ireland","5":"UEFA","6":"68","7":"146","8":"0.47","9":"1998–2016","10":"4 June 2011","11":"[66]"},{"1":"NA","2":"30","3":"Harry Kane","4":"England","5":"UEFA","6":"66","7":"98","8":"0.67","9":"2015–","10":"7 June 2022","11":"[67]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_C%C3%B4te_d%27Ivoire.svg","2":"31","3":"Didier Drogba","4":"Ivory Coast","5":"CAF","6":"65","7":"105","8":"0.62","9":"2002–2014","10":"13 January 2012","11":"[68]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/b/bf/Flag_of_Bosnia_and_Herzegovina.svg","2":"31","3":"Edin Džeko","4":"Bosnia and Herzegovina","5":"UEFA","6":"65","7":"134","8":"0.49","9":"2007–","10":"28 March 2017","11":"[69]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/a9/Flag_of_Thailand.svg","2":"33","3":"Teerasil Dangda","4":"Thailand","5":"AFC","6":"64","7":"128","8":"0.50","9":"2007–","10":"14 December 2021","11":"[70]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/aa/Flag_of_Kuwait.svg","2":"34","3":"Jasem Al-Huwaidi","4":"Kuwait","5":"AFC","6":"63","7":"83","8":"0.76","9":"1992–2003","10":"30 September 2000","11":"[71]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"35","3":"Ronaldo","4":"Brazil","5":"CONMEBOL","6":"62","7":"98","8":"0.63","9":"1994–2011","10":"19 November 2003","11":"[72]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg","2":"35","3":"Ahmed Radhi","4":"Iraq","5":"AFC","6":"62","7":"121","8":"0.51","9":"1982–1997","10":"18 August 1992","11":"[73]"},{"1":"https://upload.wikimedia.org/wikipedia/en/4/4c/Flag_of_Sweden.svg","2":"35","3":"Zlatan Ibrahimović","4":"Sweden","5":"UEFA","6":"62","7":"122","8":"0.51","9":"2001–2023","10":"4 September 2014","11":"[74]"},{"1":"NA","2":"38","3":"Abdul Ghani Minhat","4":"Malaya Malaysia","5":"AFC","6":"61","7":"71","8":"0.86","9":"1956–1966","10":"15 December 1961","11":"[75]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"39","3":"Imre Schlosser","4":"Hungary","5":"UEFA","6":"59","7":"68","8":"0.87","9":"1906–1927","10":"3 June 1917","11":"[9]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9a/Flag_of_Spain.svg","2":"39","3":"David Villa","4":"Spain","5":"UEFA","6":"59","7":"98","8":"0.60","9":"2005–2017","10":"11 October 2011","11":"[76]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/ff/Flag_of_Serbia.svg","2":"41","3":"Aleksandar Mitrović","4":"Serbia","5":"UEFA","6":"58","7":"94","8":"0.62","9":"2013–","10":"27 September 2022","11":"[77]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/0f/Flag_of_Maldives.svg","2":"41","3":"Ali Ashfaq","4":"Maldives","5":"AFC","6":"58","7":"98","8":"0.59","9":"2003–","10":"29 March 2016","11":"[78]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/09/Flag_of_South_Korea.svg","2":"41","3":"Cha Bum-kun","4":"South Korea","5":"AFC","6":"58","7":"136","8":"0.43","9":"1972–1986","10":"5 September 1977","11":"[79]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Uruguay.svg","2":"41","3":"Edinson Cavani","4":"Uruguay","5":"CONMEBOL","6":"58","7":"136","8":"0.43","9":"2008–2022","10":"18 November 2019","11":"[80]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg","2":"45","3":"Mohamed Salah","4":"Egypt","5":"CAF","6":"57","7":"100","8":"0.57","9":"2011–","10":"24 March 2023","11":"[81]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/8/82/Flag_of_Honduras.svg","2":"45","3":"Carlos Pavón","4":"Honduras","5":"CONCACAF","6":"57","7":"101","8":"0.56","9":"1993–2010","10":"28 March 2009","11":"[82]"},{"1":"https://upload.wikimedia.org/wikipedia/en/c/c3/Flag_of_France.svg","2":"45","3":"Olivier Giroud","4":"France","5":"UEFA","6":"57","7":"137","8":"0.42","9":"2011–2024","10":"22 November 2022","11":"[83]"},{"1":"https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg","2":"45","3":"Clint Dempsey","4":"United States","5":"CONCACAF","6":"57","7":"141","8":"0.40","9":"2004–2018","10":"7 June 2016","11":"[84]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg","2":"45","3":"Younis Mahmoud","4":"Iraq","5":"AFC","6":"57","7":"148","8":"0.39","9":"2002–2016","10":"5 March 2014","11":"[85]"},{"1":"https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg","2":"45","3":"Landon Donovan","4":"United States","5":"CONCACAF","6":"57","7":"157","8":"0.36","9":"2000–2014","10":"5 July 2013","11":"[86]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg","2":"51","3":"Gabriel Batistuta","4":"Argentina","5":"CONMEBOL","6":"56","7":"78","8":"0.72","9":"1991–2002","10":"29 June 2000","11":"[87]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/4/4f/Flag_of_Cameroon.svg","2":"51","3":"Samuel Eto'o","4":"Cameroon","5":"CAF","6":"56","7":"118","8":"0.47","9":"1997–2014","10":"3 September 2011","11":"[88]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/aa/Flag_of_Kuwait.svg","2":"51","3":"Bader Al-Mutawa","4":"Kuwait","5":"AFC","6":"56","7":"196","8":"0.29","9":"2003–2022","10":"3 September 2015","11":"[6]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"54","3":"Romário","4":"Brazil","5":"CONMEBOL","6":"55","7":"70","8":"0.79","9":"1987–2005","10":"8 October 2000","11":"[91]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9e/Flag_of_Japan.svg","2":"54","3":"Kazuyoshi Miura","4":"Japan","5":"AFC","6":"55","7":"89","8":"0.62","9":"1990–2000","10":"7 September 1997","11":"[92]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_Czech_Republic.svg","2":"54","3":"Jan Koller","4":"Czech Republic","5":"UEFA","6":"55","7":"91","8":"0.60","9":"1999–2009","10":"8 September 2007","11":"[93]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9f/Flag_of_Indonesia.svg","2":"54","3":"Iswadi Idris","4":"Indonesia","5":"AFC","6":"55","7":"97","8":"0.57","9":"1968–1980","10":"19 November 1977","11":"[94]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/4/48/Flag_of_Singapore.svg","2":"54","3":"Fandi Ahmad","4":"Singapore","5":"AFC","6":"55","7":"101","8":"0.54","9":"1979–1997","10":"16 December 1995","11":"[95]"},{"1":"NA","2":"54","3":"Joachim Streich","4":"East Germany","5":"UEFA","6":"55","7":"102","8":"0.54","9":"1969–1984","10":"26 July 1983","11":"[96]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/65/Flag_of_Qatar.svg","2":"60","3":"Almoez Ali","4":"Qatar","5":"AFC","6":"54","7":"112","8":"0.48","9":"2013–","10":"31 December 2023","11":"[97][98]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"61","3":"Sardar Azmoun","4":"Iran","5":"AFC","6":"53","7":"83","8":"0.64","9":"2014–","10":"14 January 2024","11":"[99]"},{"1":"NA","2":"61","3":"Wayne Rooney","4":"England","5":"UEFA","6":"53","7":"120","8":"0.44","9":"2003–2018","10":"8 September 2015","11":"[100]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9c/Flag_of_Denmark.svg","2":"63","3":"Poul Nielsen","4":"Denmark","5":"UEFA","6":"52","7":"38","8":"1.37","9":"1910–1925","10":"14 June 1925","11":"[12]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/99/Flag_of_the_Philippines.svg","2":"63","3":"Phil Younghusband","4":"Philippines","5":"AFC","6":"52","7":"108","8":"0.48","9":"2006–2019","10":"22 March 2018","11":"[101]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fc/Flag_of_Mexico.svg","2":"63","3":"Javier Hernández","4":"Mexico","5":"CONCACAF","6":"52","7":"109","8":"0.48","9":"2009–2019","10":"23 June 2018","11":"[102]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9c/Flag_of_Denmark.svg","2":"63","3":"Jon Dahl Tomasson","4":"Denmark","5":"UEFA","6":"52","7":"112","8":"0.46","9":"1997–2010","10":"21 November 2007","11":"[103]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg","2":"63","3":"Adnan Al Talyani","4":"United Arab Emirates","5":"AFC","6":"52","7":"161","8":"0.32","9":"1983–1997","10":"19 November 1996","11":"[104]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"68","3":"Lajos Tichy","4":"Hungary","5":"UEFA","6":"51","7":"72","8":"0.71","9":"1955–1971","10":"25 April 1964","11":"[105]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/2/21/Flag_of_Vietnam.svg","2":"68","3":"Lê Công Vinh","4":"Vietnam","5":"AFC","6":"51","7":"83","8":"0.61","9":"2004–2016","10":"20 November 2016","11":"[106]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/1/19/Flag_of_Ghana.svg","2":"68","3":"Asamoah Gyan","4":"Ghana","5":"CAF","6":"51","7":"109","8":"0.47","9":"2003–2019","10":"11 June 2017","11":"[107]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/b/b4/Flag_of_Turkey.svg","2":"68","3":"Hakan Şükür","4":"Turkey","5":"UEFA","6":"51","7":"112","8":"0.46","9":"1992–2007","10":"11 October 2006","11":"[108]"},{"1":"https://upload.wikimedia.org/wikipedia/en/c/c3/Flag_of_France.svg","2":"68","3":"Thierry Henry","4":"France","5":"UEFA","6":"51","7":"123","8":"0.41","9":"1997–2010","10":"9 September 2009","11":"[109]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/7/78/Flag_of_Chile.svg","2":"68","3":"Alexis Sánchez","4":"Chile","5":"CONMEBOL","6":"51","7":"166","8":"0.31","9":"2006–","10":"27 September 2022","11":"[110]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"74","3":"Mehdi Taremi","4":"Iran","5":"AFC","6":"50","7":"87","8":"0.57","9":"2015–","10":"6 June 2024","11":"[111][112]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"74","3":"Karim Bagheri","4":"Iran","5":"AFC","6":"50","7":"87","8":"0.57","9":"1993–2010","10":"9 January 2009","11":"[113]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/2/20/Flag_of_the_Netherlands.svg","2":"74","3":"Robin van Persie","4":"Netherlands","5":"UEFA","6":"50","7":"102","8":"0.49","9":"2005–2017","10":"13 October 2015","11":"[114]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/09/Flag_of_South_Korea.svg","2":"74","3":"Hwang Sun-hong","4":"South Korea","5":"AFC","6":"50","7":"103","8":"0.49","9":"1988–2002","10":"4 June 2002","11":"[115]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/8/88/Flag_of_Australia_%28converted%29.svg","2":"74","3":"Tim Cahill","4":"Australia","5":"AFC / OFC[h]","6":"50","7":"108","8":"0.46","9":"2004–2018","10":"10 October 2017","11":"[120]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9e/Flag_of_Japan.svg","2":"74","3":"Shinji Okazaki","4":"Japan","5":"AFC","6":"50","7":"119","8":"0.42","9":"2008–2019","10":"28 March 2017","11":"[121]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg","2":"74","3":"Zainal Abidin Hassan","4":"Malaysia","5":"AFC","6":"50","7":"129","8":"0.39","9":"1980–1997","10":"31 March 1997","11":"[122]"}],"options":{"columns":{"min":{},"max":[10],"total":[11]},"rows":{"min":[10],"max":[10],"total":[80]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


I need to recode one of the confederation values so that it's clean for the by confederation table.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibnJvdyI6ODAsIm5jb2wiOjExLCJzdW1tYXJ5Ijp7IkEgdGliYmxlIjpbIjgwIMOXIDExIl19fSwicmRmIjoiSDRzSUFBQUFBQUFBQTlWY3kyL2NTSHJ2dFMwL0pGbVdad2FMQkFFbVRBSm5kdzkyTjlrdk1zaEFsaVhyTFZ1amxqM2owWGprNm1hcG15TTIyY09ITkZJdXZpeHkzRU5PeVNISUlMa2toOFVDeVdFUGc4Qlk3ZjREU1lCTk5zbkdNN3ZaU1RKQmdoeDJqK3Q4Sk9zcmZxUzZiYlVsQTRrQXVzaGkxZS83ZmM4aWl3MnZ6NzViSG4xM3RGQW9uQzJjT3dmL2pzQnBZZVRleHR4MXZWQTRkd1l1dmxJNFY3Z1V0Ui9EN2RmaFpBeU9TVGpXeEkyRlRoRDAvTjhwRnNPZTdUTHp4cDYxWTNXNWFiRWJydGN1UmxlOTZLclljcnRkMS9HTDFXSzFWWnl6V1h2TDNkNWFjNzBnYkRQN2hyL2JGbmlMUStLcFJaVkp2R212elozQWNoZ0JuQjBTc0ZWc3BZQ0xIbk1JMXMxalluR25XQ2xXMUJUR2ljYWtPTU1hclZhczFTVFlLclBadnAvQmUzZDRIWnNTTCtqd3JYdU9GWEFUN01lYVc3ZTdsc2NDN2hQOHhwRDRSdEhRSlA0dGJyZXRzTHQxVGROYjFxNWxYOU1NQWowL1BQWFVyZ3VoMDJiZVBvR2JQcjZISUhJMEVvazJjMHdDTkRja3IxS3hsTHJvUGRadFpodzBCQzBBcXFhMjg5aUJaWjhnbXJlTDJ6VWF6UitkTHFsQzRkSXorSHMxdmh3aTJ5RGd1RVJhWXIxTTFnN3JTbFprYVFWWUR2ZVlGUkMwbGVFRHc1Um9EUmFhVnB4bW1mQVlscUZaTk5WTVBkaXpUbEJkUUY5RG9tMTBtSlZMaFZ2SDkwT3oyRXhOTjgrOUxuUDJYeUd6WVJjTENKTnRXcFJkaDJjTDZiQ0ZEZ3B6SlNYb1dZNWxNbk1MU0c1dHVFM1dkZ24wN2VFek53M3AyKzM5WG5DQ3Fwa0J1K2VGN1pEdDkwbmdZZTNKaXp4ZHpPZERXRFc2RUl3WjRLeUFqWlB3bnJrMlU3NTJxeEx3TGZPYVZsL2NkUzJQRTV2Y0h4SWJZalVOaGx1dTcxZ3M5dHdDOXc1NDI5M05Qa2FjZHVpZWJsSDYvNzYrd05OU0draU5QVzV5NS8vYStwSmF2OUZqMWtuV0Y3QlpHbmdON21YWGdtRUREZnk1VGRjQzA5ck5QTHN0RDQrWEJtN0REWVBPMXJMcmNmWXFxczhycUl6RG1rOHY2dWxUNElMcm1LSEgvSmNMWWdpM3NvU2FnemVIRm4rSjV3WUFnbHhQVnhYeWVONEljcy9scDVtdHI0TGZxYi9NRGV0ZHFDdHBjc3l3THZkYzk5VTlHcDVhRlQ2dEo5LzFrNzRYemh6d1ZtZHJuZmZDcG0yMVh1V1QxN0NBNEZrOUxWTVcxUGFlS3g0SHNvdkdzTlVGSHVsU3o3ek5BdWFkK21iQ3lWWTFNR1c2VnM1eXA4dThIVUx4N3ZCd1JzYm5heDNMdG5vOXk4bWs4a3NzY2luTFZmNngxWEpQc0lLOFFPZFh2Zjl4eWc4ZXc4SnBSUzJGdTIveHdHSGRFNnlmVUdWVGo4OTNtSE9TVjFGNGlpWnZRS0czdzE5eU8rYjVxK2V3T3RhTDliUTh6RUJFODFQUDR0UEhHaloxSVM1S21UQyt3K0ZmTDNyVGVNVlBnQStHZjhwSzNURWQrb0hIYkhqZGlyWUVYV2VYZTVCODJXM0IwMW9CVDIrbnRWQzRIRzk3UjN2aWhjS1plTk84QUZJS2hXalgvTHc0TGtiRkhZNVJjWXlMZVJPNTR6VTRYaWZIVjhueHErTDROWEs4Q2NldmkrTTM0UGhOT0g2TEhMOE54OWZFOFkzY2NYM0FVU1pIYmNEeHUzQzhKWTZwUHNmc2dHUHBPY2RrSWYxOGNIWEdzL3pBWW82cnJMc092TDI0NHNiNGlnWFBDTGF5eW4zZkVuMFhwMjFMbVdVY3J5ODNRc2V5bFpsT2h3Y2VkazZzdWpzZFdMVmhZSWZKM3ZGbzZpcHI3blFnbm5INnV0dmxkcWlzaER0c0p5d1VIc2ZUNTdqSG5aYXlGdm83aDUvNFl1aHI2MjRUb2xSWjRYdVFYTzZldjRQQVYrWmRjOXZqKzhEQ0NwZ2RpdTd6ZC9nK0xGSW9hU0gwZlc0NVNvTnhiZ3BKSTJ2Y1B2eHpGSERmMmdVcktPKzRycm5IUEhQVGZJaUVHb2VmZ0VoUFdYWmJ2aVVKTFlQcWZzZHFjMldaZFZuWERkQndWMjR4SHhSWHBwdG1hTnVzSTgzQ1B1Um12bmQ4MlhJYzFsRmd6WmVtZW0zWllvSGxoenRLZzhOQ0V6S25MVEVzei9WdHRxc3MyNjdQVWVDYXRROFBYMDRiYk1hdnU0N29Ib3RGQVR2VFFqT01OZ0x1T2NxUzIzR2tZVnpmWjExbGdVSGpDSTNIVjBMTFZ4cmg0U2NlUDhDK2VlNlp5dXJocDdiTkVXNXNobm5BUTFrUHJRUFVCL3pVdE1BbW5EbkliM1NCZWQ0K0VKRTlsMmN0MCtJUUlaN2JiakloWWV5MkNRNmEvY0ZmOHgxcHlnM080VzBRUW13V2pHQXkwVDI1eEh6ZVZhYnQ2d3ZSRzRDSmhydVFqZUN4NlE1VUdtV2RtUjFMeUhqOVBSc2VLQjFsc2VteGp0VjFkNjN2L3o1YVBURlh0QnhEb0ZwT2gyR1lUaXgyUGE0MFdoM1ExVStWbjJXN2xxbmN0OENiQXYyTmFadnZnQmxOOFA2cUZYZ1VmalNLLzJtL3M4MCtrdGJyTU9WVzJMMitFNkkzSmlJVCtLNmp6TEJkb0lIV1duVTdMTktrd2FMQVNXUmRGclpmWTd1SGZ5bm4zN1VoaXNHdzh4QW5vWW56WjJ6TENaUlozdTM1ZkIrSFBuQ2pBSWFVN0hUVG9STXJVWGFCRjF6SEJRWllJK1paMDdPZ0Z0eUs0aklJQTNURWVBUENFL3B2Qis3WFNQaWJ3QUNjc3dvRDk5QTJGeUhYSVo0c09XeVpIWVQ3TG1RUW1BcGUrZEZNUytDZFpaY0UyZmlpdndjaHJDeWFua3krc1RtZ0NlYnNkQmt5djdMa3NoYTRWR2tFSHJkYW5kVHNYWmNmQUoyMFprRjJSK2w1QUhxamh1UHZzSDJIUXdXRWtvY1dHbDl6SVI3dWdONCtsNWFJbnMyVnlIVHRUdWczZ1lWUTcrb1NpdzIvQVBrVmxRdU9DWEYxS1RJbjY5aktodHVGSkpQcE9UbHRPcURyTk54ZzluN3E3YkVWOWlINGRRTjAyTWNLdEhMNEY4ck00VjlCaHQrSHdKUVZGUkxYaGRveHZ5OHpkMktCN1FEb0QvNzQ4Tk9kdzA5bDlkdm9BRGRJd1FYdWVBaDZCWUwxNHlqTmdXNnJJL21Pci9JT21IYURlYndyVGJZTWRid0wzbS9Ed3cxMlRrS21RNzVDbENocjNQTXR6TzJKQmFqUWJhZ2V6dldPS3l2WDZBWUF6RURPMlRhT2EzUXM1ME5MdWJ2RERwaXM1bSs4eHl6SVlTaVRWbFFOc0N4bGxxeUwrTlZhWEYrU0d4V2k0MXowV0NmT1IrSlB2emdUSHloUVd2TGFvVVN2SFFxK2RtQXhFWjlOOFZLOFJlRHlrbnl2eEt2a2V5TmVKZHNKaE14SGZlLzh5bTJuSFlFbzJNSTZFdkRROC91TEhJa2ZyUkFwMmZ0STh6Q004aUgrcklVamtzOVNxRG51Z0NPMitEWTA0UFlsdVVNZ09sN0hieXRLUkRUNXRvSzg0aDFBeEJXN2l6S3Z1QjhvV1ZtWDVIY0t4TWJ0RGNYZFZoWTlUbWtLMDJCdUxPNjZFTVl6THZOUjRGZVREd2N4TGZMaFlJQmVXYk05eDFISkZqaldsamhzbUpLTG5yeC80bTFwQ1JCdks1TzRpN2VGVVkvNG9WNkpIK3I3R3k1ajFJdTRMWXJneWRzWlpxY0k0bVR6cjQ4eWZRY2NTWnFMdUR0M0RGTmxRbkVpM3FOUzBJbURJdWlTM0NQQzJMak5qc1RHU0x6ZjB5ZU5jNEZ3UVd4Qm9EM0psb2tNLzNqTG8vLzQ1K1o5MXFzWHhPcytFb3hmMTFGRzhycmQxeXNqOFR0dkgwM28rUmg1WHh3Y0dwZmsrMW8vODZjMUxWc2x6OTI3UFRjdGZYdjN6dXJ0VzNkWHhQWFo2Ym1aNDU1U25FSG5aMmVtNTE0c0tuOXJJTm9MMmFYaUJoRHRQeThpTUROTkpnK21uYmNlblhZTUt4eVB5d0E3RFpoOExFY2NUMVpXNzBHNkhUSFhZRXMrUjhLSmRIN3BFUU5HUDAvZFk4aDZjUXdjTDlPR2kvYm9OTm0wV0x2NTZHWWgrcnU1aVcwaGFkOTVuTFQzUmYrOWZDdkdiVHhKMmthK0ZmTWJZdno2a3hlMEF1L3RKd1BheHdQYW03bTIwTDlkRStQWGJ1WmFjZit1dUgrMzBMKzlJKzZ2NXR2Qzg5dVZ4ME8yaGY3dDh1TWhXekZ2NlhHdUxSeXZYWHc4WkZ0NHFiYUFjZmlod0drL1N0cW11RzQrVFZyMkpHbmZGKzFEMFdKOHRnVHVwdWgvSks2WmtyVHZvSDRDRitPaUlkcEhpSHN6MjJJLzRqekl5VUUrMjBxV0o4Yk5vejhSZWdpOGQ0WDg5M0w0eUJmekNjZDlJTVo5Z0x5ZlpQbmpPTXhYdkdhRmJJdThIOXpNNnNPUW41alhFdGVZdnc5RjIwSDVva1c3MzBlK043UDREOFM0OTNONmZTQ3VaMFNMOVFickQ0NDNCYi8xM1B6OHVBOUV2eW5hZTdrV2VUekErV0lleHMralJFNUJ4T0hVVDc3NTVuZmYvdktiVTU5LzYvMnYvL3g3MzVyNkltN2VuL3JKRDBmZjZ2M3BENmQrR2w5K1krcUxiNzl4OE5uOHQ2ZCtGbzErODd0VC94VmZ2akgxMlI5R2YzOGsrM0hlNTlHL28yOU4vVWMwNnVDenFWK0krLzhqeHYrM3dQc3M2bjM3UCtVODVQTTBFdnYxWDB3OWpWQjZmemIxcyszNFQvTEJjWDh2eHYyTDRJMzRUMk54NjFNL0Zqei9OYWJ6a1pTRDQ1OG14cGo2TnpFZThYRSt0bDhLZVY4aXozTDhsK29yOVB4SE1RNWJ0QVBxK1NNeDdoOEVUK1Nmd0l4T2ZTRmE1UDAzd2kvL0hrOWJTTzBrNUV0OGNSL2JId3Q3L3pTRytiMnBmeEo2L1Z6d3dQdlkvck93ejkrSjhkS2ZRZy9rZytOK0pPVCtiYzdmMktKOXNaWHpoUDVDN3dJK2N5ZDdLaGUwVXFuOCtlTS9JSmZWOUhKTU5Zem9MdlRXc0V1TTBFcGFKUjFWMTZCTE5mUXF3VEV5c0dvcEExdXB4aE5xR3BtZ1owYlU5QVN5TkJDalhvOUhHS1cwcTVwMDFWWGNYVktOV0QzVlVDdnAvbmdrUDBHdjFvakFTakszVHBTdkpjclhqd3FseWljU2RQV28xZXJFYW1yY3BaS0p1cHBnRWZpYVVNQWdXSW01VlkxTXJHYWRFbG12bnJWZUxjRWgwZ3c5d2FrTjdvcHNUTjBQc0ZxV2RVN1NVY0ZHTXFGVUpsMlZCSVBZUjlkeW1rdjdhR1JpTlZHaVJoaVhraTZOVGhUMnFSTWxjaUZkenNhTkNGWWEwb2toTkJLT3F0b3ZEOVJTT2tsVmMza0FPRUpWL2FnRnFiVFNrVkF3RXF3U2NiSlJ6NDBTaWhDYWtTV1RVYVVxbVpqQWwwaGVHRWJTUmNJcW4xK1JZWXlqOFpoMDZaV0J4bFVyMllBcDV5d0FxVmRLZkZZbG81TEVVZzNTWmVTNlVnc1FpbnI1Q01WcU5adnp4QTIxbzd3b3ZIWWt1L01TTHdpcUEvS2piMWprNHpGaXJlZTgyejlTOUNNVTlaSlVON05WTXE3VmxLWFE0VW9jSDJMVFRET1VWZWExT2txc3VkanFNcFFsNW9UTTIxZmlpRWg2Sjh1cU1zdGJ2TnZrWGpTNmlxTTFUWmtPMjZFZktHQlFpUUdqUlcvTUx1bTlvcGFVdTYzQUZSQ0daRllCWnZZK0FGUTFCS2pTa1hVRXFDdDMzTjJFQTBqVGtadXFwdjFFazh0cVhhZ1hoNlBZZTVMQ2FsWENkcFZGWFNVakt2bEo3MVhWVUJxOEY2QzRLaUtNcXpwQzFKSHZwRmFsNWlscGtrSlZtZTU1bHAyaFVKUHpVWVVyV3BsYVhaV21xVXVub1NldWxFdHlLSUNpRlMvcnhBK2FwRnJHK2FVS29UckhtNTRBTUhRWkRPVTBHUFNNcmdCQVFDY2luYVJ6TldyWGhDbXlINVBrTlUyR0FOVlRUcjZzNmFuc3VuUnJoZHBVUTlpcllJRFVNVFJHd1dNa0RtQkJRY0xFTm9aMFdTV0RJcE5pVWlXdWhDaVIycFRSRW1rOFF1Q1JNSlVFd1dzVVdrdlY3Sk52azlWTW1OVlQ5ZlZNVkV0SFE3b2dpRmJ1WThDU0lUMnRVUVJKSS9XTEpERmVUWW5KTUswbVlSclZieG1QaG95bnRESms3YWdPNkpmWnBoT2JwU2oxakJVTWFRVTk2K3Q2UDE5bnJGYWozak9xa3JsTU9yMHNHV1pxbWpUbUZRaThORWkxU244cVVxRnh0WUtSb1ZXbFA3USt5YVRKYkpSOWsxcW1kZzNTejVBMVRVc0xTaTFONlZMZkFqZ084WWtDKzhkc1NVYWhrYld6OGFKWUhwUExpVFJRZHVWSXEzNlpKZ2xhS0swWHBiUTRsUHBWL2I3RjRYSmNzNVBhZm1TdHU3Q3BQZHdzNjFqSnoyMldEVHdmMzlTcUR6Y3JKVGpVOUg2bGt0NVhkYmlYakVudjE4aDVQVDFYS1FhUlZ6SFM4eXJCcVpMeDVTcWVYOXhVNnc4M3ExcDZUNlB6SytTOFNzNEpwekk1cnhKK1ZjS3BTakJyaEZPNW52S29xUTgzYTRSSHJVek9DWThhNFZFanNtdEVkbzNJcmhIWmRTSzdUdXhSSjNMclJHNmR5SzFMdVdjM0tTU2hVQ2NVNm9SQ25ZelhDUVdkVU5BSkJaMVEwQWtGbmFpdUU3azZrYXZyS1UweXhDQ2lEQ0xLSUtJTUlzb2dvZ3lKYzNIVGdHZ3hpR3FHVkcxa1V5MFIzVlNOM2xEcFJlWk9tVjVVNkVXVlh0VG9SWjFlNlBTQ3NsRWxtMUc0Z09oU001eFVLbG1sa2xVcVdTdlJDNnFIQm1qWi8wTmd4R0ZkN291Q01JWTIyNDUrYkhsdlhYNzU4cGlEMzBuUDkyeTJMMytKYzk1aGdTVy9EMTl1dWM0Mk43bEhPMGZhTHJQbE4rZ1c2K0g1Ukh5ang3MnRMZ3ZrcjNQR1dzemowT2VubnpPdm1pemcwVzgvcTZXZ3N4WE53bkR4K0haT24wdWV1M2NEZFlwKzVIbm1NZnp6N05tejcrUVZiOW5NUjhXeGN4UWtzUnZiSHN5SHExL21wbHh3ZTVGZU1PbE05UFBRODduSlgvRnlIVmRDSjJKaVhtOTFRbWNuK3U4Yk1yZlA5cHpvRjZ5amhlVFhxd1ZCT0RwZkkrZGpDWXN6ejhUMDgyaDY3clF0K2ZPNUVaczF1YlNMeVhmUnlHQ1AyQnczWUJWMDhOUDlLUFQ2TndJM2tLWWNiYmsyOXNTYUYzNzV2OG1QTDQrS1FnQUEifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["flag_URL"],"name":[1],"type":["chr"],"align":["left"]},{"label":["rank"],"name":[2],"type":["int"],"align":["right"]},{"label":["player"],"name":[3],"type":["chr"],"align":["left"]},{"label":["nation"],"name":[4],"type":["chr"],"align":["left"]},{"label":["confederation"],"name":[5],"type":["chr"],"align":["left"]},{"label":["goals"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["caps"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["goalsper_match"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["career_span"],"name":[9],"type":["chr"],"align":["left"]},{"label":["date_of_50th_goal"],"name":[10],"type":["chr"],"align":["left"]},{"label":["ref"],"name":[11],"type":["chr"],"align":["left"]}],"data":[{"1":"https://upload.wikimedia.org/wikipedia/commons/5/5c/Flag_of_Portugal.svg","2":"1","3":"Cristiano Ronaldo","4":"Portugal","5":"UEFA","6":"130","7":"212","8":"0.61","9":"2003–","10":"26 June 2014","11":"[2][38]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg","2":"2","3":"Lionel Messi","4":"Argentina","5":"CONMEBOL","6":"109","7":"187","8":"0.58","9":"2005–","10":"29 March 2016","11":"[39]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"3","3":"Ali Daei","4":"Iran","5":"AFC","6":"108","7":"148","8":"0.73","9":"1993–2006","10":"9 January 2000","11":"[25][40][41]"},{"1":"https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg","2":"4","3":"Sunil Chhetri","4":"India","5":"AFC","6":"94","7":"151","8":"0.62","9":"2005–2024","10":"31 December 2015","11":"[44]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg","2":"5","3":"Mokhtar Dahari","4":"Malaysia","5":"AFC","6":"89","7":"142","8":"0.63","9":"1972–1985","10":"22 August 1976","11":"[18][45][40]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg","2":"6","3":"Ali Mabkhout","4":"United Arab Emirates","5":"AFC","6":"85","7":"115","8":"0.74","9":"2009–","10":"31 August 2019","11":"[46]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/92/Flag_of_Belgium_%28civil%29.svg","2":"6","3":"Romelu Lukaku","4":"Belgium","5":"UEFA","6":"85","7":"119","8":"0.71","9":"2010–","10":"10 October 2019","11":"[47]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"8","3":"Ferenc Puskás","4":"Hungary","5":"UEFA","6":"84","7":"89","8":"0.94","9":"1945–1962","10":"24 July 1952","11":"[11]"},{"1":"https://upload.wikimedia.org/wikipedia/en/1/12/Flag_of_Poland.svg","2":"9","3":"Robert Lewandowski","4":"Poland","5":"UEFA","6":"83","7":"152","8":"0.55","9":"2008–","10":"5 October 2017","11":"[48]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/06/Flag_of_Zambia.svg","2":"10","3":"Godfrey Chitalu","4":"Zambia","5":"CAF","6":"79","7":"111","8":"0.71","9":"1968–1980","10":"7 November 1978","11":"[49]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"10","3":"Neymar","4":"Brazil","5":"CONMEBOL","6":"79","7":"128","8":"0.62","9":"2010–","10":"11 November 2016","11":"[50]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg","2":"12","3":"Hussein Saeed","4":"Iraq","5":"AFC","6":"78","7":"137","8":"0.57","9":"1977–1990","10":"17 March 1984","11":"[51]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"13","3":"Pelé","4":"Brazil","5":"CONMEBOL","6":"77","7":"92","8":"0.84","9":"1957–1971","10":"4 July 1965","11":"[35]"},{"1":"NA","2":"14","3":"Vivian Woodward[d]","4":"England England amateurs","5":"UEFA","6":"75","7":"53","8":"1.42","9":"1903–1914[d]","10":"31 May 1909[d]","11":"[17][52]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"14","3":"Sándor Kocsis","4":"Hungary","5":"UEFA","6":"75","7":"68","8":"1.10","9":"1948–1956","10":"19 September 1954","11":"[29]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9e/Flag_of_Japan.svg","2":"14","3":"Kunishige Kamamoto","4":"Japan","5":"AFC","6":"75","7":"76","8":"0.99","9":"1964–1977","10":"18 July 1972","11":"[54]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/aa/Flag_of_Kuwait.svg","2":"14","3":"Bashar Abdullah","4":"Kuwait","5":"AFC","6":"75","7":"134","8":"0.56","9":"1996–2007","10":"25 December 2002","11":"[55]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/0d/Flag_of_Saudi_Arabia.svg","2":"18","3":"Majed Abdullah","4":"Saudi Arabia","5":"AFC","6":"72","7":"117","8":"0.62","9":"1977–1994","10":"15 April 1984","11":"[56]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/d/d1/Flag_of_Malawi.svg","2":"19","3":"Kinnah Phiri","4":"Malawi","5":"CAF","6":"71","7":"117","8":"0.61","9":"1973–1981","10":"6 July 1978","11":"[36]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/a9/Flag_of_Thailand.svg","2":"19","3":"Kiatisuk Senamuang","4":"Thailand","5":"AFC","6":"71","7":"134","8":"0.53","9":"1993–2007","10":"23 January 2001","11":"[57]"},{"1":"https://upload.wikimedia.org/wikipedia/en/b/ba/Flag_of_Germany.svg","2":"19","3":"Miroslav Klose","4":"Germany","5":"UEFA","6":"71","7":"137","8":"0.52","9":"2001–2014","10":"27 June 2010","11":"[58]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/a9/Flag_of_Thailand.svg","2":"22","3":"Piyapong Pue-on","4":"Thailand","5":"AFC","6":"70","7":"100","8":"0.70","9":"1981–1997","10":"30 January 1989","11":"[59]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9f/Flag_of_Indonesia.svg","2":"22","3":"Abdul Kadir","4":"Indonesia","5":"AFC","6":"70","7":"111","8":"0.63","9":"1967–1979","10":"8 August 1972","11":"[60]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/64/Flag_of_Trinidad_and_Tobago.svg","2":"22","3":"Stern John","4":"Trinidad and Tobago","5":"CONCACAF","6":"70","7":"115","8":"0.61","9":"1995–2012","10":"13 June 2004","11":"[37]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg","2":"25","3":"Hossam Hassan","4":"Egypt","5":"CAF","6":"69","7":"177","8":"0.39","9":"1985–2006","10":"25 February 1998","11":"[61][62]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Uruguay.svg","2":"25","3":"Luis Suárez","4":"Uruguay","5":"CONMEBOL","6":"69","7":"142","8":"0.49","9":"2007–","10":"23 March 2018","11":"[63]"},{"1":"NA","2":"27","3":"Gerd Müller","4":"West Germany","5":"UEFA","6":"68","7":"62","8":"1.10","9":"1966–1974","10":"18 June 1972","11":"[64]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/e/ec/Flag_of_Guatemala.svg","2":"27","3":"Carlos Ruiz","4":"Guatemala","5":"CONCACAF","6":"68","7":"133","8":"0.51","9":"1998–2016","10":"15 August 2012","11":"[65]"},{"1":"NA","2":"27","3":"Robbie Keane","4":"Republic of Ireland","5":"UEFA","6":"68","7":"146","8":"0.47","9":"1998–2016","10":"4 June 2011","11":"[66]"},{"1":"NA","2":"30","3":"Harry Kane","4":"England","5":"UEFA","6":"66","7":"98","8":"0.67","9":"2015–","10":"7 June 2022","11":"[67]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_C%C3%B4te_d%27Ivoire.svg","2":"31","3":"Didier Drogba","4":"Ivory Coast","5":"CAF","6":"65","7":"105","8":"0.62","9":"2002–2014","10":"13 January 2012","11":"[68]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/b/bf/Flag_of_Bosnia_and_Herzegovina.svg","2":"31","3":"Edin Džeko","4":"Bosnia and Herzegovina","5":"UEFA","6":"65","7":"134","8":"0.49","9":"2007–","10":"28 March 2017","11":"[69]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/a9/Flag_of_Thailand.svg","2":"33","3":"Teerasil Dangda","4":"Thailand","5":"AFC","6":"64","7":"128","8":"0.50","9":"2007–","10":"14 December 2021","11":"[70]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/aa/Flag_of_Kuwait.svg","2":"34","3":"Jasem Al-Huwaidi","4":"Kuwait","5":"AFC","6":"63","7":"83","8":"0.76","9":"1992–2003","10":"30 September 2000","11":"[71]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"35","3":"Ronaldo","4":"Brazil","5":"CONMEBOL","6":"62","7":"98","8":"0.63","9":"1994–2011","10":"19 November 2003","11":"[72]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg","2":"35","3":"Ahmed Radhi","4":"Iraq","5":"AFC","6":"62","7":"121","8":"0.51","9":"1982–1997","10":"18 August 1992","11":"[73]"},{"1":"https://upload.wikimedia.org/wikipedia/en/4/4c/Flag_of_Sweden.svg","2":"35","3":"Zlatan Ibrahimović","4":"Sweden","5":"UEFA","6":"62","7":"122","8":"0.51","9":"2001–2023","10":"4 September 2014","11":"[74]"},{"1":"NA","2":"38","3":"Abdul Ghani Minhat","4":"Malaya Malaysia","5":"AFC","6":"61","7":"71","8":"0.86","9":"1956–1966","10":"15 December 1961","11":"[75]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"39","3":"Imre Schlosser","4":"Hungary","5":"UEFA","6":"59","7":"68","8":"0.87","9":"1906–1927","10":"3 June 1917","11":"[9]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9a/Flag_of_Spain.svg","2":"39","3":"David Villa","4":"Spain","5":"UEFA","6":"59","7":"98","8":"0.60","9":"2005–2017","10":"11 October 2011","11":"[76]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/ff/Flag_of_Serbia.svg","2":"41","3":"Aleksandar Mitrović","4":"Serbia","5":"UEFA","6":"58","7":"94","8":"0.62","9":"2013–","10":"27 September 2022","11":"[77]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/0f/Flag_of_Maldives.svg","2":"41","3":"Ali Ashfaq","4":"Maldives","5":"AFC","6":"58","7":"98","8":"0.59","9":"2003–","10":"29 March 2016","11":"[78]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/09/Flag_of_South_Korea.svg","2":"41","3":"Cha Bum-kun","4":"South Korea","5":"AFC","6":"58","7":"136","8":"0.43","9":"1972–1986","10":"5 September 1977","11":"[79]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Uruguay.svg","2":"41","3":"Edinson Cavani","4":"Uruguay","5":"CONMEBOL","6":"58","7":"136","8":"0.43","9":"2008–2022","10":"18 November 2019","11":"[80]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg","2":"45","3":"Mohamed Salah","4":"Egypt","5":"CAF","6":"57","7":"100","8":"0.57","9":"2011–","10":"24 March 2023","11":"[81]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/8/82/Flag_of_Honduras.svg","2":"45","3":"Carlos Pavón","4":"Honduras","5":"CONCACAF","6":"57","7":"101","8":"0.56","9":"1993–2010","10":"28 March 2009","11":"[82]"},{"1":"https://upload.wikimedia.org/wikipedia/en/c/c3/Flag_of_France.svg","2":"45","3":"Olivier Giroud","4":"France","5":"UEFA","6":"57","7":"137","8":"0.42","9":"2011–2024","10":"22 November 2022","11":"[83]"},{"1":"https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg","2":"45","3":"Clint Dempsey","4":"United States","5":"CONCACAF","6":"57","7":"141","8":"0.40","9":"2004–2018","10":"7 June 2016","11":"[84]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg","2":"45","3":"Younis Mahmoud","4":"Iraq","5":"AFC","6":"57","7":"148","8":"0.39","9":"2002–2016","10":"5 March 2014","11":"[85]"},{"1":"https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg","2":"45","3":"Landon Donovan","4":"United States","5":"CONCACAF","6":"57","7":"157","8":"0.36","9":"2000–2014","10":"5 July 2013","11":"[86]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg","2":"51","3":"Gabriel Batistuta","4":"Argentina","5":"CONMEBOL","6":"56","7":"78","8":"0.72","9":"1991–2002","10":"29 June 2000","11":"[87]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/4/4f/Flag_of_Cameroon.svg","2":"51","3":"Samuel Eto'o","4":"Cameroon","5":"CAF","6":"56","7":"118","8":"0.47","9":"1997–2014","10":"3 September 2011","11":"[88]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/a/aa/Flag_of_Kuwait.svg","2":"51","3":"Bader Al-Mutawa","4":"Kuwait","5":"AFC","6":"56","7":"196","8":"0.29","9":"2003–2022","10":"3 September 2015","11":"[6]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"54","3":"Romário","4":"Brazil","5":"CONMEBOL","6":"55","7":"70","8":"0.79","9":"1987–2005","10":"8 October 2000","11":"[91]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9e/Flag_of_Japan.svg","2":"54","3":"Kazuyoshi Miura","4":"Japan","5":"AFC","6":"55","7":"89","8":"0.62","9":"1990–2000","10":"7 September 1997","11":"[92]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_Czech_Republic.svg","2":"54","3":"Jan Koller","4":"Czech Republic","5":"UEFA","6":"55","7":"91","8":"0.60","9":"1999–2009","10":"8 September 2007","11":"[93]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9f/Flag_of_Indonesia.svg","2":"54","3":"Iswadi Idris","4":"Indonesia","5":"AFC","6":"55","7":"97","8":"0.57","9":"1968–1980","10":"19 November 1977","11":"[94]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/4/48/Flag_of_Singapore.svg","2":"54","3":"Fandi Ahmad","4":"Singapore","5":"AFC","6":"55","7":"101","8":"0.54","9":"1979–1997","10":"16 December 1995","11":"[95]"},{"1":"NA","2":"54","3":"Joachim Streich","4":"East Germany","5":"UEFA","6":"55","7":"102","8":"0.54","9":"1969–1984","10":"26 July 1983","11":"[96]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/65/Flag_of_Qatar.svg","2":"60","3":"Almoez Ali","4":"Qatar","5":"AFC","6":"54","7":"112","8":"0.48","9":"2013–","10":"31 December 2023","11":"[97][98]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"61","3":"Sardar Azmoun","4":"Iran","5":"AFC","6":"53","7":"83","8":"0.64","9":"2014–","10":"14 January 2024","11":"[99]"},{"1":"NA","2":"61","3":"Wayne Rooney","4":"England","5":"UEFA","6":"53","7":"120","8":"0.44","9":"2003–2018","10":"8 September 2015","11":"[100]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9c/Flag_of_Denmark.svg","2":"63","3":"Poul Nielsen","4":"Denmark","5":"UEFA","6":"52","7":"38","8":"1.37","9":"1910–1925","10":"14 June 1925","11":"[12]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/99/Flag_of_the_Philippines.svg","2":"63","3":"Phil Younghusband","4":"Philippines","5":"AFC","6":"52","7":"108","8":"0.48","9":"2006–2019","10":"22 March 2018","11":"[101]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fc/Flag_of_Mexico.svg","2":"63","3":"Javier Hernández","4":"Mexico","5":"CONCACAF","6":"52","7":"109","8":"0.48","9":"2009–2019","10":"23 June 2018","11":"[102]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/9c/Flag_of_Denmark.svg","2":"63","3":"Jon Dahl Tomasson","4":"Denmark","5":"UEFA","6":"52","7":"112","8":"0.46","9":"1997–2010","10":"21 November 2007","11":"[103]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg","2":"63","3":"Adnan Al Talyani","4":"United Arab Emirates","5":"AFC","6":"52","7":"161","8":"0.32","9":"1983–1997","10":"19 November 1996","11":"[104]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"68","3":"Lajos Tichy","4":"Hungary","5":"UEFA","6":"51","7":"72","8":"0.71","9":"1955–1971","10":"25 April 1964","11":"[105]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/2/21/Flag_of_Vietnam.svg","2":"68","3":"Lê Công Vinh","4":"Vietnam","5":"AFC","6":"51","7":"83","8":"0.61","9":"2004–2016","10":"20 November 2016","11":"[106]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/1/19/Flag_of_Ghana.svg","2":"68","3":"Asamoah Gyan","4":"Ghana","5":"CAF","6":"51","7":"109","8":"0.47","9":"2003–2019","10":"11 June 2017","11":"[107]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/b/b4/Flag_of_Turkey.svg","2":"68","3":"Hakan Şükür","4":"Turkey","5":"UEFA","6":"51","7":"112","8":"0.46","9":"1992–2007","10":"11 October 2006","11":"[108]"},{"1":"https://upload.wikimedia.org/wikipedia/en/c/c3/Flag_of_France.svg","2":"68","3":"Thierry Henry","4":"France","5":"UEFA","6":"51","7":"123","8":"0.41","9":"1997–2010","10":"9 September 2009","11":"[109]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/7/78/Flag_of_Chile.svg","2":"68","3":"Alexis Sánchez","4":"Chile","5":"CONMEBOL","6":"51","7":"166","8":"0.31","9":"2006–","10":"27 September 2022","11":"[110]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"74","3":"Mehdi Taremi","4":"Iran","5":"AFC","6":"50","7":"87","8":"0.57","9":"2015–","10":"6 June 2024","11":"[111][112]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"74","3":"Karim Bagheri","4":"Iran","5":"AFC","6":"50","7":"87","8":"0.57","9":"1993–2010","10":"9 January 2009","11":"[113]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/2/20/Flag_of_the_Netherlands.svg","2":"74","3":"Robin van Persie","4":"Netherlands","5":"UEFA","6":"50","7":"102","8":"0.49","9":"2005–2017","10":"13 October 2015","11":"[114]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/09/Flag_of_South_Korea.svg","2":"74","3":"Hwang Sun-hong","4":"South Korea","5":"AFC","6":"50","7":"103","8":"0.49","9":"1988–2002","10":"4 June 2002","11":"[115]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/8/88/Flag_of_Australia_%28converted%29.svg","2":"74","3":"Tim Cahill","4":"Australia","5":"AFC","6":"50","7":"108","8":"0.46","9":"2004–2018","10":"10 October 2017","11":"[120]"},{"1":"https://upload.wikimedia.org/wikipedia/en/9/9e/Flag_of_Japan.svg","2":"74","3":"Shinji Okazaki","4":"Japan","5":"AFC","6":"50","7":"119","8":"0.42","9":"2008–2019","10":"28 March 2017","11":"[121]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg","2":"74","3":"Zainal Abidin Hassan","4":"Malaysia","5":"AFC","6":"50","7":"129","8":"0.39","9":"1980–1997","10":"31 March 1997","11":"[122]"}],"options":{"columns":{"min":{},"max":[10],"total":[11]},"rows":{"min":[10],"max":[10],"total":[80]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



# Data Prep

First, I'll choose the top 12 scorers.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGZfdG9wX3Njb3JlcnMgPC0gcmF3ICU+JSBcbiAgc2xpY2UoMToxMilcbmBgYCJ9 -->

```r
df_top_scorers <- raw %>% 
  slice(1:12)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Then, I'll extract the min and max values from the table for conditional formatting of the table.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubWluX2dvYWxzIDwtIGRmX3RvcF9zY29yZXJzJGdvYWxzICU+JSBtaW4oKVxubWF4X2dvYWxzIDwtIGRmX3RvcF9zY29yZXJzJGdvYWxzICU+JSBtYXgoKVxuXG5nb2Fsc19wYWxldHRlIDwtIGNvbF9udW1lcmljKGMoXCJsaWdodGdyZWVuXCIsIFwiZGFya2dyZWVuXCIpLCBcbiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgZG9tYWluID0gYyhtaW5fZ29hbHMsIG1heF9nb2FscyksIFxuICAgICAgICAgICAgICAgICAgICAgICAgICAgICBhbHBoYSA9IC43NSlcbmBgYCJ9 -->

```r
min_goals <- df_top_scorers$goals %>% min()
max_goals <- df_top_scorers$goals %>% max()

goals_palette <- col_numeric(c("lightgreen", "darkgreen"), 
                             domain = c(min_goals, max_goals), 
                             alpha = .75)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuKHRibF90b3Bfc2NvcmVycyA8LSBkZl90b3Bfc2NvcmVycyAlPiUgXG4gIHNlbGVjdChyYW5rLCBwbGF5ZXIsIGNhcmVlcl9zcGFuLCBmbGFnX1VSTCwgbmF0aW9uLCBnb2FscywgY2FwcywgZ29hbHNwZXJfbWF0Y2gpICU+JSBcbiAgZ3QoKSAlPiUgXG4gICNyZW5hbWUgY29sdW1uc1xuICBjb2xzX2xhYmVsKHJhbmsgPSAnUmFuaycsXG4gICAgICAgICAgICAgcGxheWVyID0gJ05hbWUnLFxuICAgICAgICAgICAgIGNhcmVlcl9zcGFuID0gJ0NhcmVlciBTcGFuJyxcbiAgICAgICAgICAgICBuYXRpb24gPSAnQ291bnRyeScsXG4gICAgICAgICAgICAgZ29hbHMgPSAnVG90YWwgR29hbHMgU2NvcmVkJyxcbiAgICAgICAgICAgICBjYXBzID0gJ01hdGNoZXMnLFxuICAgICAgICAgICAgIGdvYWxzcGVyX21hdGNoID0gJ0dvYWxzIHBlciBNYXRjaCcpICU+JSBcbiAgI2FkZCB0YWJsZSB0aXRsZVxuICB0YWJfaGVhZGVyKHRpdGxlID0gbWQoXCIqKlRvdGFsIEdvYWxzIFNjb3JlZCBpbiBNZW4ncyBJbnRlcm5hdGlvbmFsIFNvY2NlciBNYXRjaGVzKipcIikpICU+JSBcbiAgdGFiX3NvdXJjZV9ub3RlKHNvdXJjZV9ub3RlID0gXCJEYXRhIGZyb20gV2lraXBlZGlhXCIpICU+JSBcbiAgI2FwcGx5IG5ldyBzdHlsZSB0byBhbGwgY29sdW1uIGhlYWRlcnNcbiAgdGFiX3N0eWxlKFxuICAgIGxvY2F0aW9ucyA9IGNlbGxzX2NvbHVtbl9sYWJlbHMoY29sdW1ucyA9IGV2ZXJ5dGhpbmcoKSksXG4gICAgc3R5bGUgPSBsaXN0KFxuICAgICAgI3RoaWNrIGJvcmRlclxuICAgICAgY2VsbF9ib3JkZXJzKHNpZGVzID0gXCJib3R0b21cIiwgd2VpZ2h0ID0gcHgoMykpLFxuICAgICAgI21ha2UgdGV4dCBib2xkXG4gICAgICBjZWxsX3RleHQod2VpZ2h0ID0gXCJib2xkXCIpXG4gICAgKVxuICApICU+JSBcbiAgI2FwcGx5IGRpZmZlcmVudCBzdHlsZSB0byB0aXRsZVxuICB0YWJfc3R5bGUobG9jYXRpb25zID0gY2VsbHNfdGl0bGUoZ3JvdXBzID0gXCJ0aXRsZVwiKSxcbiAgICAgICAgICAgIHN0eWxlID0gbGlzdChcbiAgICAgICAgICAgICAgY2VsbF90ZXh0KHdlaWdodCA9IFwiYm9sZFwiLCBzaXplID0gMjQpXG4gICAgICAgICAgICApKSAlPiUgXG4gIGRhdGFfY29sb3IoY29sdW1ucyA9IGMoZ29hbHMpLFxuICAgICAgICAgICAgIGNvbG9ycyA9IGdvYWxzX3BhbGV0dGUpICU+JSBcbiAgb3B0X2FsbF9jYXBzKCkgJT4lIFxuICBvcHRfdGFibGVfZm9udChcbiAgICBmb250ID0gbGlzdChcbiAgICAgIGdvb2dsZV9mb250KFwiQ2hpdm9cIiksXG4gICAgICBkZWZhdWx0X2ZvbnRzKClcbiAgICApXG4gICkgJT4lIFxuICB0YWJfb3B0aW9ucyhcbiAgICAjcmVtb3ZlIGJvcmRlciBiZXR3ZWVuIGNvbHVtbiBoZWFkZXJzIGFuZCB0aXRsZVxuICAgIGNvbHVtbl9sYWJlbHMuYm9yZGVyLnRvcC53aWR0aCA9IHB4KDMpLFxuICAgIGNvbHVtbl9sYWJlbHMuYm9yZGVyLnRvcC5jb2xvciA9IFwidHJhbnNwYXJlbnRcIixcbiAgICAjcmVtb3ZlIGJvcmRlciBhcm91bmQgdGhlIHRhYmxlXG4gICAgdGFibGUuYm9yZGVyLnRvcC5jb2xvciA9IFwidHJhbnNwYXJlbnRcIixcbiAgICB0YWJsZS5ib3JkZXIuYm90dG9tLmNvbG9yID0gXCJ0cmFuc3BhcmVudFwiLFxuICAgICNhZGp1c3QgZm9udCBzaXplcyBhbmQgYWxpZ25tZW50XG4gICAgc291cmNlX25vdGVzLmZvbnQuc2l6ZSA9IDEyLFxuICAgIGhlYWRpbmcuYWxpZ24gPSBcImxlZnRcIlxuICApKVxuYGBgIn0= -->

```r
(tbl_top_scorers <- df_top_scorers %>% 
  select(rank, player, career_span, flag_URL, nation, goals, caps, goalsper_match) %>% 
  gt() %>% 
  #rename columns
  cols_label(rank = 'Rank',
             player = 'Name',
             career_span = 'Career Span',
             nation = 'Country',
             goals = 'Total Goals Scored',
             caps = 'Matches',
             goalsper_match = 'Goals per Match') %>% 
  #add table title
  tab_header(title = md("**Total Goals Scored in Men's International Soccer Matches**")) %>% 
  tab_source_note(source_note = "Data from Wikipedia") %>% 
  #apply new style to all column headers
  tab_style(
    locations = cells_column_labels(columns = everything()),
    style = list(
      #thick border
      cell_borders(sides = "bottom", weight = px(3)),
      #make text bold
      cell_text(weight = "bold")
    )
  ) %>% 
  #apply different style to title
  tab_style(locations = cells_title(groups = "title"),
            style = list(
              cell_text(weight = "bold", size = 24)
            )) %>% 
  data_color(columns = c(goals),
             colors = goals_palette) %>% 
  opt_all_caps() %>% 
  opt_table_font(
    font = list(
      google_font("Chivo"),
      default_fonts()
    )
  ) %>% 
  tab_options(
    #remove border between column headers and title
    column_labels.border.top.width = px(3),
    column_labels.border.top.color = "transparent",
    #remove border around the table
    table.border.top.color = "transparent",
    table.border.bottom.color = "transparent",
    #adjust font sizes and alignment
    source_notes.font.size = 12,
    heading.align = "left"
  ))
```

<!-- rnb-source-end -->

```{=html}

<!-- rnb-html-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInNoaW55LnRhZyJdLCJzaXppbmdQb2xpY3kiOltdfX0= -->

<div id="lwmhcyqboy" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
  <style>@import url("https://fonts.googleapis.com/css2?family=Chivo:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
#lwmhcyqboy table {
  font-family: Chivo, system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#lwmhcyqboy thead, #lwmhcyqboy tbody, #lwmhcyqboy tfoot, #lwmhcyqboy tr, #lwmhcyqboy td, #lwmhcyqboy th {
  border-style: none;
}

#lwmhcyqboy p {
  margin: 0;
  padding: 0;
}

#lwmhcyqboy .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: rgba(255, 255, 255, 0);
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: rgba(255, 255, 255, 0);
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#lwmhcyqboy .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#lwmhcyqboy .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#lwmhcyqboy .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#lwmhcyqboy .gt_heading {
  background-color: #FFFFFF;
  text-align: left;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#lwmhcyqboy .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#lwmhcyqboy .gt_col_headings {
  border-top-style: solid;
  border-top-width: 3px;
  border-top-color: rgba(255, 255, 255, 0);
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#lwmhcyqboy .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#lwmhcyqboy .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#lwmhcyqboy .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#lwmhcyqboy .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#lwmhcyqboy .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#lwmhcyqboy .gt_spanner_row {
  border-bottom-style: hidden;
}

#lwmhcyqboy .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#lwmhcyqboy .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#lwmhcyqboy .gt_from_md > :first-child {
  margin-top: 0;
}

#lwmhcyqboy .gt_from_md > :last-child {
  margin-bottom: 0;
}

#lwmhcyqboy .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#lwmhcyqboy .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#lwmhcyqboy .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#lwmhcyqboy .gt_row_group_first td {
  border-top-width: 2px;
}

#lwmhcyqboy .gt_row_group_first th {
  border-top-width: 2px;
}

#lwmhcyqboy .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#lwmhcyqboy .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#lwmhcyqboy .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#lwmhcyqboy .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#lwmhcyqboy .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#lwmhcyqboy .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#lwmhcyqboy .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#lwmhcyqboy .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#lwmhcyqboy .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#lwmhcyqboy .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#lwmhcyqboy .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#lwmhcyqboy .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#lwmhcyqboy .gt_sourcenote {
  font-size: 12px;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#lwmhcyqboy .gt_left {
  text-align: left;
}

#lwmhcyqboy .gt_center {
  text-align: center;
}

#lwmhcyqboy .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#lwmhcyqboy .gt_font_normal {
  font-weight: normal;
}

#lwmhcyqboy .gt_font_bold {
  font-weight: bold;
}

#lwmhcyqboy .gt_font_italic {
  font-style: italic;
}

#lwmhcyqboy .gt_super {
  font-size: 65%;
}

#lwmhcyqboy .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#lwmhcyqboy .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#lwmhcyqboy .gt_indent_1 {
  text-indent: 5px;
}

#lwmhcyqboy .gt_indent_2 {
  text-indent: 10px;
}

#lwmhcyqboy .gt_indent_3 {
  text-indent: 15px;
}

#lwmhcyqboy .gt_indent_4 {
  text-indent: 20px;
}

#lwmhcyqboy .gt_indent_5 {
  text-indent: 25px;
}
</style>
  <table class="gt_table" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <thead>
    <tr class="gt_heading">
      <td colspan="8" class="gt_heading gt_title gt_font_normal gt_bottom_border" style="font-size: 24; font-weight: bold;"><strong>Total Goals Scored in Men’s International Soccer Matches</strong></td>
    </tr>
    
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Rank">Rank</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Name">Name</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Career Span">Career Span</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="flag_URL">flag_URL</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Country">Country</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Total Goals Scored">Total Goals Scored</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Matches">Matches</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Goals per Match">Goals per Match</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="rank" class="gt_row gt_right">1</td>
<td headers="player" class="gt_row gt_left">Cristiano Ronaldo</td>
<td headers="career_span" class="gt_row gt_left">2003–</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/5/5c/Flag_of_Portugal.svg</td>
<td headers="nation" class="gt_row gt_left">Portugal</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #006400; color: #FFFFFF;">130</td>
<td headers="caps" class="gt_row gt_right">212</td>
<td headers="goalsper_match" class="gt_row gt_right">0.61</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">2</td>
<td headers="player" class="gt_row gt_left">Lionel Messi</td>
<td headers="career_span" class="gt_row gt_left">2005–</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg</td>
<td headers="nation" class="gt_row gt_left">Argentina</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #44993D; color: #FFFFFF;">109</td>
<td headers="caps" class="gt_row gt_right">187</td>
<td headers="goalsper_match" class="gt_row gt_right">0.58</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">3</td>
<td headers="player" class="gt_row gt_left">Ali Daei</td>
<td headers="career_span" class="gt_row gt_left">1993–2006</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg</td>
<td headers="nation" class="gt_row gt_left">Iran</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #469C40; color: #FFFFFF;">108</td>
<td headers="caps" class="gt_row gt_right">148</td>
<td headers="goalsper_match" class="gt_row gt_right">0.73</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">4</td>
<td headers="player" class="gt_row gt_left">Sunil Chhetri</td>
<td headers="career_span" class="gt_row gt_left">2005–2024</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg</td>
<td headers="nation" class="gt_row gt_left">India</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #69C265; color: #000000;">94</td>
<td headers="caps" class="gt_row gt_right">151</td>
<td headers="goalsper_match" class="gt_row gt_right">0.62</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">5</td>
<td headers="player" class="gt_row gt_left">Mokhtar Dahari</td>
<td headers="career_span" class="gt_row gt_left">1972–1985</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg</td>
<td headers="nation" class="gt_row gt_left">Malaysia</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #75CF72; color: #000000;">89</td>
<td headers="caps" class="gt_row gt_right">142</td>
<td headers="goalsper_match" class="gt_row gt_right">0.63</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">6</td>
<td headers="player" class="gt_row gt_left">Ali Mabkhout</td>
<td headers="career_span" class="gt_row gt_left">2009–</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg</td>
<td headers="nation" class="gt_row gt_left">United Arab Emirates</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #7FDA7D; color: #000000;">85</td>
<td headers="caps" class="gt_row gt_right">115</td>
<td headers="goalsper_match" class="gt_row gt_right">0.74</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">6</td>
<td headers="player" class="gt_row gt_left">Romelu Lukaku</td>
<td headers="career_span" class="gt_row gt_left">2010–</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/9/92/Flag_of_Belgium_%28civil%29.svg</td>
<td headers="nation" class="gt_row gt_left">Belgium</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #7FDA7D; color: #000000;">85</td>
<td headers="caps" class="gt_row gt_right">119</td>
<td headers="goalsper_match" class="gt_row gt_right">0.71</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">8</td>
<td headers="player" class="gt_row gt_left">Ferenc Puskás</td>
<td headers="career_span" class="gt_row gt_left">1945–1962</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg</td>
<td headers="nation" class="gt_row gt_left">Hungary</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #81DD80; color: #000000;">84</td>
<td headers="caps" class="gt_row gt_right">89</td>
<td headers="goalsper_match" class="gt_row gt_right">0.94</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">9</td>
<td headers="player" class="gt_row gt_left">Robert Lewandowski</td>
<td headers="career_span" class="gt_row gt_left">2008–</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/en/1/12/Flag_of_Poland.svg</td>
<td headers="nation" class="gt_row gt_left">Poland</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #84E082; color: #000000;">83</td>
<td headers="caps" class="gt_row gt_right">152</td>
<td headers="goalsper_match" class="gt_row gt_right">0.55</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">10</td>
<td headers="player" class="gt_row gt_left">Godfrey Chitalu</td>
<td headers="career_span" class="gt_row gt_left">1968–1980</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/0/06/Flag_of_Zambia.svg</td>
<td headers="nation" class="gt_row gt_left">Zambia</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #8EEB8D; color: #000000;">79</td>
<td headers="caps" class="gt_row gt_right">111</td>
<td headers="goalsper_match" class="gt_row gt_right">0.71</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">10</td>
<td headers="player" class="gt_row gt_left">Neymar</td>
<td headers="career_span" class="gt_row gt_left">2010–</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg</td>
<td headers="nation" class="gt_row gt_left">Brazil</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #8EEB8D; color: #000000;">79</td>
<td headers="caps" class="gt_row gt_right">128</td>
<td headers="goalsper_match" class="gt_row gt_right">0.62</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">12</td>
<td headers="player" class="gt_row gt_left">Hussein Saeed</td>
<td headers="career_span" class="gt_row gt_left">1977–1990</td>
<td headers="flag_URL" class="gt_row gt_left">https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg</td>
<td headers="nation" class="gt_row gt_left">Iraq</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #90EE90; color: #000000;">78</td>
<td headers="caps" class="gt_row gt_right">137</td>
<td headers="goalsper_match" class="gt_row gt_right">0.57</td></tr>
  </tbody>
  <tfoot class="gt_sourcenotes">
    <tr>
      <td class="gt_sourcenote" colspan="8">Data from Wikipedia</td>
    </tr>
  </tfoot>
  
</table>
</div>


<!-- rnb-html-end -->

```

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuKHRibF90b3Bfc2NvcmVycyA8LSB0YmxfdG9wX3Njb3JlcnMgJT4lIFxuICAgIHRleHRfdHJhbnNmb3JtKFxuICAgICNBcHBseSBhIGZ1bmN0aW9uIHRvIGEgY29sdW1uXG4gICAgbG9jYXRpb25zID0gY2VsbHNfYm9keShjKGZsYWdfVVJMKSksXG4gICAgZm4gPSBmdW5jdGlvbih4KSB7XG4gICAgICAjUmV0dXJuIGFuIGltYWdlIG9mIHNldCBkaW1lbnNpb25zXG4gICAgICB3ZWJfaW1hZ2UoXG4gICAgICAgIHVybCA9IHgsXG4gICAgICAgIGhlaWdodCA9IDEyXG4gICAgICApXG4gICAgfVxuICApICU+JSBcbiAgI0hpZGUgY29sdW1uIGhlYWRlciBmbGFnX1VSTCBhbmQgcmVkdWNlIHdpZHRoXG4gIGNvbHNfd2lkdGgoYyhmbGFnX1VSTCkgfiBweCgzMCkpICU+JSBcbiAgY29sc19sYWJlbChmbGFnX1VSTCA9IFwiXCIpKVxuYGBgIn0= -->

```r
(tbl_top_scorers <- tbl_top_scorers %>% 
    text_transform(
    #Apply a function to a column
    locations = cells_body(c(flag_URL)),
    fn = function(x) {
      #Return an image of set dimensions
      web_image(
        url = x,
        height = 12
      )
    }
  ) %>% 
  #Hide column header flag_URL and reduce width
  cols_width(c(flag_URL) ~ px(30)) %>% 
  cols_label(flag_URL = ""))
```

<!-- rnb-source-end -->

```{=html}

<!-- rnb-html-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInNoaW55LnRhZyJdLCJzaXppbmdQb2xpY3kiOltdfX0= -->

<div id="loynmkavrf" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
  <style>@import url("https://fonts.googleapis.com/css2?family=Chivo:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
#loynmkavrf table {
  font-family: Chivo, system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#loynmkavrf thead, #loynmkavrf tbody, #loynmkavrf tfoot, #loynmkavrf tr, #loynmkavrf td, #loynmkavrf th {
  border-style: none;
}

#loynmkavrf p {
  margin: 0;
  padding: 0;
}

#loynmkavrf .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: rgba(255, 255, 255, 0);
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: rgba(255, 255, 255, 0);
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#loynmkavrf .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#loynmkavrf .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#loynmkavrf .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#loynmkavrf .gt_heading {
  background-color: #FFFFFF;
  text-align: left;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#loynmkavrf .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#loynmkavrf .gt_col_headings {
  border-top-style: solid;
  border-top-width: 3px;
  border-top-color: rgba(255, 255, 255, 0);
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#loynmkavrf .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#loynmkavrf .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#loynmkavrf .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#loynmkavrf .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#loynmkavrf .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#loynmkavrf .gt_spanner_row {
  border-bottom-style: hidden;
}

#loynmkavrf .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#loynmkavrf .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#loynmkavrf .gt_from_md > :first-child {
  margin-top: 0;
}

#loynmkavrf .gt_from_md > :last-child {
  margin-bottom: 0;
}

#loynmkavrf .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#loynmkavrf .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#loynmkavrf .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#loynmkavrf .gt_row_group_first td {
  border-top-width: 2px;
}

#loynmkavrf .gt_row_group_first th {
  border-top-width: 2px;
}

#loynmkavrf .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#loynmkavrf .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#loynmkavrf .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#loynmkavrf .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#loynmkavrf .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#loynmkavrf .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#loynmkavrf .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#loynmkavrf .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#loynmkavrf .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#loynmkavrf .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#loynmkavrf .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#loynmkavrf .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#loynmkavrf .gt_sourcenote {
  font-size: 12px;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#loynmkavrf .gt_left {
  text-align: left;
}

#loynmkavrf .gt_center {
  text-align: center;
}

#loynmkavrf .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#loynmkavrf .gt_font_normal {
  font-weight: normal;
}

#loynmkavrf .gt_font_bold {
  font-weight: bold;
}

#loynmkavrf .gt_font_italic {
  font-style: italic;
}

#loynmkavrf .gt_super {
  font-size: 65%;
}

#loynmkavrf .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#loynmkavrf .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#loynmkavrf .gt_indent_1 {
  text-indent: 5px;
}

#loynmkavrf .gt_indent_2 {
  text-indent: 10px;
}

#loynmkavrf .gt_indent_3 {
  text-indent: 15px;
}

#loynmkavrf .gt_indent_4 {
  text-indent: 20px;
}

#loynmkavrf .gt_indent_5 {
  text-indent: 25px;
}
</style>
  <table class="gt_table" style="table-layout: fixed;" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <colgroup>
    <col/>
    <col/>
    <col/>
    <col style="width:30px;"/>
    <col/>
    <col/>
    <col/>
    <col/>
  </colgroup>
  <thead>
    <tr class="gt_heading">
      <td colspan="8" class="gt_heading gt_title gt_font_normal gt_bottom_border" style="font-size: 24; font-weight: bold;"><strong>Total Goals Scored in Men’s International Soccer Matches</strong></td>
    </tr>
    
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Rank">Rank</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Name">Name</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Career Span">Career Span</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Country">Country</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Total Goals Scored">Total Goals Scored</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Matches">Matches</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Goals per Match">Goals per Match</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="rank" class="gt_row gt_right">1</td>
<td headers="player" class="gt_row gt_left">Cristiano Ronaldo</td>
<td headers="career_span" class="gt_row gt_left">2003–</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Flag_of_Portugal.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Portugal</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #006400; color: #FFFFFF;">130</td>
<td headers="caps" class="gt_row gt_right">212</td>
<td headers="goalsper_match" class="gt_row gt_right">0.61</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">2</td>
<td headers="player" class="gt_row gt_left">Lionel Messi</td>
<td headers="career_span" class="gt_row gt_left">2005–</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Argentina</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #44993D; color: #FFFFFF;">109</td>
<td headers="caps" class="gt_row gt_right">187</td>
<td headers="goalsper_match" class="gt_row gt_right">0.58</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">3</td>
<td headers="player" class="gt_row gt_left">Ali Daei</td>
<td headers="career_span" class="gt_row gt_left">1993–2006</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Iran</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #469C40; color: #FFFFFF;">108</td>
<td headers="caps" class="gt_row gt_right">148</td>
<td headers="goalsper_match" class="gt_row gt_right">0.73</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">4</td>
<td headers="player" class="gt_row gt_left">Sunil Chhetri</td>
<td headers="career_span" class="gt_row gt_left">2005–2024</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">India</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #69C265; color: #000000;">94</td>
<td headers="caps" class="gt_row gt_right">151</td>
<td headers="goalsper_match" class="gt_row gt_right">0.62</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">5</td>
<td headers="player" class="gt_row gt_left">Mokhtar Dahari</td>
<td headers="career_span" class="gt_row gt_left">1972–1985</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Malaysia</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #75CF72; color: #000000;">89</td>
<td headers="caps" class="gt_row gt_right">142</td>
<td headers="goalsper_match" class="gt_row gt_right">0.63</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">6</td>
<td headers="player" class="gt_row gt_left">Ali Mabkhout</td>
<td headers="career_span" class="gt_row gt_left">2009–</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">United Arab Emirates</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #7FDA7D; color: #000000;">85</td>
<td headers="caps" class="gt_row gt_right">115</td>
<td headers="goalsper_match" class="gt_row gt_right">0.74</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">6</td>
<td headers="player" class="gt_row gt_left">Romelu Lukaku</td>
<td headers="career_span" class="gt_row gt_left">2010–</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/9/92/Flag_of_Belgium_%28civil%29.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Belgium</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #7FDA7D; color: #000000;">85</td>
<td headers="caps" class="gt_row gt_right">119</td>
<td headers="goalsper_match" class="gt_row gt_right">0.71</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">8</td>
<td headers="player" class="gt_row gt_left">Ferenc Puskás</td>
<td headers="career_span" class="gt_row gt_left">1945–1962</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Hungary</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #81DD80; color: #000000;">84</td>
<td headers="caps" class="gt_row gt_right">89</td>
<td headers="goalsper_match" class="gt_row gt_right">0.94</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">9</td>
<td headers="player" class="gt_row gt_left">Robert Lewandowski</td>
<td headers="career_span" class="gt_row gt_left">2008–</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/1/12/Flag_of_Poland.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Poland</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #84E082; color: #000000;">83</td>
<td headers="caps" class="gt_row gt_right">152</td>
<td headers="goalsper_match" class="gt_row gt_right">0.55</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">10</td>
<td headers="player" class="gt_row gt_left">Godfrey Chitalu</td>
<td headers="career_span" class="gt_row gt_left">1968–1980</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/0/06/Flag_of_Zambia.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Zambia</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #8EEB8D; color: #000000;">79</td>
<td headers="caps" class="gt_row gt_right">111</td>
<td headers="goalsper_match" class="gt_row gt_right">0.71</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">10</td>
<td headers="player" class="gt_row gt_left">Neymar</td>
<td headers="career_span" class="gt_row gt_left">2010–</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Brazil</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #8EEB8D; color: #000000;">79</td>
<td headers="caps" class="gt_row gt_right">128</td>
<td headers="goalsper_match" class="gt_row gt_right">0.62</td></tr>
    <tr><td headers="rank" class="gt_row gt_right">12</td>
<td headers="player" class="gt_row gt_left">Hussein Saeed</td>
<td headers="career_span" class="gt_row gt_left">1977–1990</td>
<td headers="flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg" style="height:12px;"></td>
<td headers="nation" class="gt_row gt_left">Iraq</td>
<td headers="goals" class="gt_row gt_right" style="background-color: #90EE90; color: #000000;">78</td>
<td headers="caps" class="gt_row gt_right">137</td>
<td headers="goalsper_match" class="gt_row gt_right">0.57</td></tr>
  </tbody>
  <tfoot class="gt_sourcenotes">
    <tr>
      <td class="gt_sourcenote" colspan="8">Data from Wikipedia</td>
    </tr>
  </tfoot>
  
</table>
</div>


<!-- rnb-html-end -->

```

<!-- rnb-chunk-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudGJsX3RvcF9zY29yZXJzICU+JSBndHNhdmUoZmlsZW5hbWUgPSBcImdyYXBoaWNzL3RibF90b3Bfc2NvcmVycy5wbmdcIilcbmBgYCJ9 -->

```r
tbl_top_scorers %>% gtsave(filename = "graphics/tbl_top_scorers.png")
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiZmlsZTovLy8vdmFyL2ZvbGRlcnMvY2svZG1nbjhsYng2dmw4c2w4OXZsaHIwc3YwMDAwMGduL1QvL1J0bXBKVDcwY2EvZmlsZTExYzQyNDAzZTVhMS5odG1sIHNjcmVlbnNob3QgY29tcGxldGVkXG4ifQ== -->

```
file:////var/folders/ck/dmgn8lbx6vl8sl89vlhr0sv00000gn/T//RtmpJT70ca/file11c42403e5a1.html screenshot completed
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


# Top scorers by confederation or continent


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuKGRmX3Njb3JlcnNfYnlfY29uZmVkIDwtIHJhdyAlPiUgXG4gIGZpbHRlcihjb25mZWRlcmF0aW9uICE9ICdBRkMgLyBPRkNbZl0nKSAlPiUgXG4gIGZpbHRlcighaXMubmEoZ29hbHMpKSAlPiUgXG4gIGdyb3VwX2J5KGNvbmZlZGVyYXRpb24pICU+JSBcbiAgc2xpY2UoMTo1KSlcbmBgYCJ9 -->

```r
(df_scorers_by_confed <- raw %>% 
  filter(confederation != 'AFC / OFC[f]') %>% 
  filter(!is.na(goals)) %>% 
  group_by(confederation) %>% 
  slice(1:5))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbImdyb3VwZWRfZGYiLCJ0YmxfZGYiLCJ0YmwiLCJkYXRhLmZyYW1lIl0sIm5yb3ciOjI1LCJuY29sIjoxMSwic3VtbWFyeSI6eyJBIHRpYmJsZSI6WyIyNSDDlyAxMSJdLCJHcm91cHMiOlsiY29uZmVkZXJhdGlvbiBbNV0iXX19LCJyZGYiOiJINHNJQUFBQUFBQUFBN1ZZUVcvY3hoV21iY21TVnJMaXhFYlJvRUJMb0JDUUhDd3V1ZVF1dDBDd1dxOGt5NjVreTFvcGRySVcxclBrN0M2ejNKbk5rSlFxbjN6cE9ZZWUybE9Ebm5ySnBaY2NpL3BIcEQwMWRvSVlhSXZlbW1QU1IzS0duRjBaZ2RlS0Y2Qm01cHYzdnZmZWNEanZqZmJXNzVjSzl3dUtvbHhRWm1iZzd5eDBsZG1EL2MxcnRxTE1uSWZCT1dWR1dZamIzOEQwRmVnc3duTVpucmY1eEhvL0RFZkJyelF0R3ZrVXVhdkgzc0FiWXRkRHE1VDF0SGcwaWtlYVE0ZERTZ0xOMFJ5a2JmcW8xNmJkOWsyR3lHcHcxT05jYXkvSmhZbG1hcWFlMDVCWUp1ZlptdEtuc2xZdVoyUTd5RWNud1JqZi9lbGo3R1I4WVIrM0Q0Z1hZcmRkWjZqVDNoaDZESVU0a1BpblhjT3UxaTNMYS9peHhMVTVKVmRSSytaY0g2SmhaeXp5YWRsY3pkWEhWdkxZazlnMnBvOFRaMndidlpOUktKSHRuNFdzc2RJb3JWdzNROXgyVjR6S3pTUHFNZnk2SEcxT3Z4dk5qR3lmZWNSemtkdEd4RzN2MHc3cVVZbjY1cFRVV01OT1JuMGpnbTA0aEhkMGhpL0gxbXdqSTl5aXhJMFlrbmYyOXN0LzBVaEQ1b3MrbW1ZNDhiVzhEczVwRjFMWDlQd1VxN01lSnFGSDVJV3N2N3lUOEFWYUdkZDFoaDU1L3VzZ3VuR1dQWDNBb2w2RVRsNkhYOU51T1V1ejhqMjhTMWtZOVpCL2hzK3RxbFh6TFh3ZCt6MHZHclpYRE52eGpqeC94YWllWVFraEQrU240VlpFZW9pOTRoTENmak9rb0gwNERSSWlSVm40SG43UVhrcHljcHpKSVhQSFdSeWVpL0Fzd1JObitDdDgvaGZ3WElQbkovRDhqUGZGYzU3TENxNWZKZ1ZBeWpNZjI0Sm5lU0wvejlkOVQxMUgyT1BqUzgySWVMN2E2UGR4eUFTNHZFTUgvUkF4RU95akRGMktWWGRRWjlDblVTalV0Nklnd0I1Um13aGpsNE52M0tCdWwrRVRZUFZDNUVkQy85Y2VJYWl2N3ZhOWpQUFNGZzBDTkZTM0VEUkVnT3VlNjJHd3ptaXZnd1M0US9zSWxoc3MrYWpQd1VJenhJeW90MmhmNkM0MkVQTnBvTzVGM2lORmVaeG9jbWdYSFQzNVMyYWo0WHNrVk5meGNCVGdFeEgzTnJ3b1N0UjFTdWhSNXM3U3RrY0o5dFVkSEFUQzc0dTM4Y2tRTVc1aGRoZjdULzdNQjB2YmtSZW96ZWpKcHd3LzR1SnplNVFnMzZWOCtHYURlVUhvSVVMVjhZbExlM1NJL1VqZGpnWm9FSEhDNVUzTU1ISFUzU2dZUFBrMDRLSnY3ZEVPWnFHNmpZOWpwNCtEZ2ZEdHJmZmhVMEJFdlVlcGU0eVkyM0lQSnpiQlRGekk4ZjVzVW8ySjNTR3FLVDYrbWg3QWFsd0pxYUlTa2tnK0ZzdVJWaUppbEZZU3drQ1NZTVhyZ2R6TllHTlFGSVF2bXI4aUVxZ0tRYWxwQXVWVEMxa0NGTTZLQkNZV2p6dWJab3NmQWhleUZDQThUbys1RjQ3bStHSDZ3c2w1Y2FJSllYNGlpU0UvUllSdWVoVHcwVTgzU0M4ZXFxSkZRL0F4WXNIRTI3cFEzMnk4U3JkUjMzeUY3bnpqenUxRy9jY2Q3MnhjdjdQOUk0MW5EalkyNjFQMzA0UHc3YldXa3Z6VzdqMU8yL2ZYMHZhQXQwMk9OLythdG5kRnkrZDNlYnZONWU2S1ZobkhKOXVXNE9kOHpiVngzanRjLytHRVB3Y2MzK2Q2ZTJtYnhkUGgvSjB2MHhaeHVRZThSU3EzejhlSG5MZkw4US81K0FObFhPL2hIem5PNXhFZk83enRQZVJ5WE8rZU1tNy9QdmZySTk0ZWNseXN0OFBsYnowZWk2ZjIvTUU3Ly92Ykp3OXFYMzFSZUcvMHB5OXFYeWZEZDJ2UFA3djY2T21OejJyUFlyVHdYdTJieisvKys3Yy8vN3oyRmZ5Qlh1M3ZzZGc3MzJaNlFrN01mNW1JNzlXZXhzM2QvOVQrOGZ2NDk0ZGFLbDZvUGZza01aenAvd3VNZ2NYYVA3ay93Zy9CSit6L04zSHJhdTBwNS9zMnhSWHhCYWNuK0tKZXJaYWVQZjZkVVN5V0JRUjlLNEVNTTVlcUdBRHBWZHZpMEJ4SVZRR1NKQ3FKUkxXWVEyVTdWWktnU2ltRjlCeXlyZE1PR0Fta203azFYUit6VmsyVmRFT0M3QlFxbjRwTkwwclVaZ3JaRWxROFpTMVpBY2w0Y2N5NGxZWmEwU1dGeXJoNzNJb3NVZm9oU3ROS0tNdUdwR0RuRXN0NnRaaXVuRzZlenByTFZmVVdJaEVjNTJvY0RVY3ZsM1NvSWh3OGhHd011RzRKYWNOUTY1QTRnbENGR01vQ0JXbU9nbXhWSkNtOUFvVVZjL29nYXB1aWlxcW90K2xSeWdzTXRzaWdaZlZXNUovSTBHWERVamR4aHlXdXhXOUlNT2dseVdONGlkeWFZWEpyc1BsS29zaUpaU09DNDlDRUI4dTZKVG1icTl1WmVsRkVzRmdSMnJvSWRkRktIUVdvbEtsV005Vk03ckt1NTRISytxWUl0R3hsK3FWY1A0dGVyOHI2eFN3aW81ejVsSzJwWGxUdk9DSGxwcXFaYUdiTEVtRXVXN0prUlhwL095Z1dMRlpQNzVDbGxtRWR0c3dpUFBxaHlEOHQwenpNNW5VYjVsS1pmTDZjOXkxWnI1cjNTNW5NZkt1c0g3YktSajVYdHZPK0xlbVhLcEtNSmNsSXVyWXA5U1UvU3BKdFMvSzFKUEdVUzNtL2tuSE90WXpEVmtseXlaVGMwT1h3N0R3a3ZYTFlzb0JpL0orWXM0NFAxd0sreGdJc3VDaEVxMTBHZDRFSjhRVkdqMWNKNExGS2ZDYzZIeWNYdUc0OW4rUVZRakh2b25DaUcxL1hEdmF5T2dOSzVJR28yMFpRRldNbVJnU0ZjQ01RZTlLaHBJdGR6R1J3dGtlUm54WEtEaHFKL25JeU1jS3NEYldlSTY0eGl3NWlHTEJnbEpYbGIwS1lPTDQ5V3NXdzM0NjFSS25HY0JlYTd5WmltcU9qMkQ1RWRUNitPbDZjV0xWemJBSjRJeUx4S3JqWG5INUVCdGVNaWVrTEl4TGZWZ3RLZXFOVStJcWVVOUticHVndnBsN01mTS9WTDRvbHdxVG5FU3hXdzBjZG5QbnY0aU94R1BEQ2tsZXhPb0txWDF3QkNvQUdxeUVOczVBTER2VUZra1N1ZlBkL1BkZU9GZ3NYQUFBPSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["flag_URL"],"name":[1],"type":["chr"],"align":["left"]},{"label":["rank"],"name":[2],"type":["int"],"align":["right"]},{"label":["player"],"name":[3],"type":["chr"],"align":["left"]},{"label":["nation"],"name":[4],"type":["chr"],"align":["left"]},{"label":["confederation"],"name":[5],"type":["chr"],"align":["left"]},{"label":["goals"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["caps"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["goalsper_match"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["career_span"],"name":[9],"type":["chr"],"align":["left"]},{"label":["date_of_50th_goal"],"name":[10],"type":["chr"],"align":["left"]},{"label":["ref"],"name":[11],"type":["chr"],"align":["left"]}],"data":[{"1":"https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg","2":"3","3":"Ali Daei","4":"Iran","5":"AFC","6":"108","7":"148","8":"0.73","9":"1993–2006","10":"9 January 2000","11":"[25][40][41]"},{"1":"https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg","2":"4","3":"Sunil Chhetri","4":"India","5":"AFC","6":"94","7":"151","8":"0.62","9":"2005–2024","10":"31 December 2015","11":"[44]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg","2":"5","3":"Mokhtar Dahari","4":"Malaysia","5":"AFC","6":"89","7":"142","8":"0.63","9":"1972–1985","10":"22 August 1976","11":"[18][45][40]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg","2":"6","3":"Ali Mabkhout","4":"United Arab Emirates","5":"AFC","6":"85","7":"115","8":"0.74","9":"2009–","10":"31 August 2019","11":"[46]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg","2":"12","3":"Hussein Saeed","4":"Iraq","5":"AFC","6":"78","7":"137","8":"0.57","9":"1977–1990","10":"17 March 1984","11":"[51]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/0/06/Flag_of_Zambia.svg","2":"10","3":"Godfrey Chitalu","4":"Zambia","5":"CAF","6":"79","7":"111","8":"0.71","9":"1968–1980","10":"7 November 1978","11":"[49]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/d/d1/Flag_of_Malawi.svg","2":"19","3":"Kinnah Phiri","4":"Malawi","5":"CAF","6":"71","7":"117","8":"0.61","9":"1973–1981","10":"6 July 1978","11":"[36]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg","2":"25","3":"Hossam Hassan","4":"Egypt","5":"CAF","6":"69","7":"177","8":"0.39","9":"1985–2006","10":"25 February 1998","11":"[61][62]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_C%C3%B4te_d%27Ivoire.svg","2":"31","3":"Didier Drogba","4":"Ivory Coast","5":"CAF","6":"65","7":"105","8":"0.62","9":"2002–2014","10":"13 January 2012","11":"[68]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg","2":"45","3":"Mohamed Salah","4":"Egypt","5":"CAF","6":"57","7":"100","8":"0.57","9":"2011–","10":"24 March 2023","11":"[81]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/6/64/Flag_of_Trinidad_and_Tobago.svg","2":"22","3":"Stern John","4":"Trinidad and Tobago","5":"CONCACAF","6":"70","7":"115","8":"0.61","9":"1995–2012","10":"13 June 2004","11":"[37]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/e/ec/Flag_of_Guatemala.svg","2":"27","3":"Carlos Ruiz","4":"Guatemala","5":"CONCACAF","6":"68","7":"133","8":"0.51","9":"1998–2016","10":"15 August 2012","11":"[65]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/8/82/Flag_of_Honduras.svg","2":"45","3":"Carlos Pavón","4":"Honduras","5":"CONCACAF","6":"57","7":"101","8":"0.56","9":"1993–2010","10":"28 March 2009","11":"[82]"},{"1":"https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg","2":"45","3":"Clint Dempsey","4":"United States","5":"CONCACAF","6":"57","7":"141","8":"0.40","9":"2004–2018","10":"7 June 2016","11":"[84]"},{"1":"https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg","2":"45","3":"Landon Donovan","4":"United States","5":"CONCACAF","6":"57","7":"157","8":"0.36","9":"2000–2014","10":"5 July 2013","11":"[86]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg","2":"2","3":"Lionel Messi","4":"Argentina","5":"CONMEBOL","6":"109","7":"187","8":"0.58","9":"2005–","10":"29 March 2016","11":"[39]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"10","3":"Neymar","4":"Brazil","5":"CONMEBOL","6":"79","7":"128","8":"0.62","9":"2010–","10":"11 November 2016","11":"[50]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"13","3":"Pelé","4":"Brazil","5":"CONMEBOL","6":"77","7":"92","8":"0.84","9":"1957–1971","10":"4 July 1965","11":"[35]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Uruguay.svg","2":"25","3":"Luis Suárez","4":"Uruguay","5":"CONMEBOL","6":"69","7":"142","8":"0.49","9":"2007–","10":"23 March 2018","11":"[63]"},{"1":"https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg","2":"35","3":"Ronaldo","4":"Brazil","5":"CONMEBOL","6":"62","7":"98","8":"0.63","9":"1994–2011","10":"19 November 2003","11":"[72]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/5/5c/Flag_of_Portugal.svg","2":"1","3":"Cristiano Ronaldo","4":"Portugal","5":"UEFA","6":"130","7":"212","8":"0.61","9":"2003–","10":"26 June 2014","11":"[2][38]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/9/92/Flag_of_Belgium_%28civil%29.svg","2":"6","3":"Romelu Lukaku","4":"Belgium","5":"UEFA","6":"85","7":"119","8":"0.71","9":"2010–","10":"10 October 2019","11":"[47]"},{"1":"https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg","2":"8","3":"Ferenc Puskás","4":"Hungary","5":"UEFA","6":"84","7":"89","8":"0.94","9":"1945–1962","10":"24 July 1952","11":"[11]"},{"1":"https://upload.wikimedia.org/wikipedia/en/1/12/Flag_of_Poland.svg","2":"9","3":"Robert Lewandowski","4":"Poland","5":"UEFA","6":"83","7":"152","8":"0.55","9":"2008–","10":"5 October 2017","11":"[48]"},{"1":"NA","2":"14","3":"Vivian Woodward[d]","4":"England England amateurs","5":"UEFA","6":"75","7":"53","8":"1.42","9":"1903–1914[d]","10":"31 May 1909[d]","11":"[17][52]"}],"options":{"columns":{"min":{},"max":[10],"total":[11]},"rows":{"min":[10],"max":[10],"total":[25]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubWluX2dvYWxzIDwtIGRmX3Njb3JlcnNfYnlfY29uZmVkJGdvYWxzICU+JSBtaW4obmEucm0gPSBUUlVFKVxubWF4X2dvYWxzIDwtIGRmX3Njb3JlcnNfYnlfY29uZmVkJGdvYWxzICU+JSBtYXgobmEucm0gPSBUUlVFKVxuXG5nb2Fsc19wYWxldHRlIDwtIGNvbF9udW1lcmljKGMoXCJsaWdodGdyZWVuXCIsIFwiZGFya2dyZWVuXCIpLCBcbiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgZG9tYWluID0gYyhtaW5fZ29hbHMsIG1heF9nb2FscyksIFxuICAgICAgICAgICAgICAgICAgICAgICAgICAgICBhbHBoYSA9IC43NSlcbmBgYCJ9 -->

```r
min_goals <- df_scorers_by_confed$goals %>% min(na.rm = TRUE)
max_goals <- df_scorers_by_confed$goals %>% max(na.rm = TRUE)

goals_palette <- col_numeric(c("lightgreen", "darkgreen"), 
                             domain = c(min_goals, max_goals), 
                             alpha = .75)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuKHRibF9zY29yZXJzX2J5X2NvbmZlZCA8LSBkZl9zY29yZXJzX2J5X2NvbmZlZCAlPiUgXG4gIHNlbGVjdChyYW5rLCBwbGF5ZXIsIGNhcmVlcl9zcGFuLCBmbGFnX1VSTCwgbmF0aW9uLCBnb2FscywgY2FwcywgZ29hbHNwZXJfbWF0Y2gsIGNvbmZlZGVyYXRpb24pICU+JSBcbiAgZ3QoZ3JvdXBuYW1lX2NvbCA9IFwiY29uZmVkZXJhdGlvblwiKSAlPiUgXG4gICAgY29sc19sYWJlbChyYW5rID0gJ0dsb2JhbCBSYW5rJyxcbiAgICAgICAgICAgICBwbGF5ZXIgPSAnTmFtZScsXG4gICAgICAgICAgICAgY2FyZWVyX3NwYW4gPSAnQ2FyZWVyIFNwYW4nLFxuICAgICAgICAgICAgIG5hdGlvbiA9ICdDb3VudHJ5JyxcbiAgICAgICAgICAgICBnb2FscyA9ICdUb3RhbCBHb2FscyBTY29yZWQnLFxuICAgICAgICAgICAgIGNhcHMgPSAnTWF0Y2hlcycsXG4gICAgICAgICAgICAgZ29hbHNwZXJfbWF0Y2ggPSAnR29hbHMgcGVyIE1hdGNoJykgJT4lIFxuICAjYWRkIHRhYmxlIHRpdGxlXG4gIHRhYl9oZWFkZXIodGl0bGUgPSBtZChcIioqVG90YWwgR29hbHMgU2NvcmVkIGluIE1lbidzIEludGVybmF0aW9uYWwgU29jY2VyIE1hdGNoZXMqKlwiKSkgJT4lIFxuICB0YWJfc291cmNlX25vdGUoc291cmNlX25vdGUgPSBcIkRhdGEgZnJvbSBXaWtpcGVkaWFcIikgJT4lIFxuICAjYXBwbHkgbmV3IHN0eWxlIHRvIGFsbCBjb2x1bW4gaGVhZGVyc1xuICB0YWJfc3R5bGUoXG4gICAgbG9jYXRpb25zID0gY2VsbHNfY29sdW1uX2xhYmVscyhjb2x1bW5zID0gZXZlcnl0aGluZygpKSxcbiAgICBzdHlsZSA9IGxpc3QoXG4gICAgICAjdGhpY2sgYm9yZGVyXG4gICAgICBjZWxsX2JvcmRlcnMoc2lkZXMgPSBcImJvdHRvbVwiLCB3ZWlnaHQgPSBweCgzKSksXG4gICAgICAjbWFrZSB0ZXh0IGJvbGRcbiAgICAgIGNlbGxfdGV4dCh3ZWlnaHQgPSBcImJvbGRcIilcbiAgICApXG4gICkgJT4lIFxuICAjYXBwbHkgZGlmZmVyZW50IHN0eWxlIHRvIHRpdGxlXG4gIHRhYl9zdHlsZShsb2NhdGlvbnMgPSBjZWxsc190aXRsZShncm91cHMgPSBcInRpdGxlXCIpLFxuICAgICAgICAgICAgc3R5bGUgPSBsaXN0KFxuICAgICAgICAgICAgICBjZWxsX3RleHQod2VpZ2h0ID0gXCJib2xkXCIsIHNpemUgPSAyNClcbiAgICAgICAgICAgICkpICU+JSBcbiAgZGF0YV9jb2xvcihjb2x1bW5zID0gYyhnb2FscyksXG4gICAgICAgICAgICAgY29sb3JzID0gZ29hbHNfcGFsZXR0ZSkgJT4lIFxuICBvcHRfYWxsX2NhcHMoKSAlPiUgXG4gIG9wdF90YWJsZV9mb250KFxuICAgIGZvbnQgPSBsaXN0KFxuICAgICAgZ29vZ2xlX2ZvbnQoXCJDaGl2b1wiKSxcbiAgICAgIGRlZmF1bHRfZm9udHMoKVxuICAgIClcbiAgKSAlPiUgXG4gIHRhYl9vcHRpb25zKFxuICAgICNyZW1vdmUgYm9yZGVyIGJldHdlZW4gY29sdW1uIGhlYWRlcnMgYW5kIHRpdGxlXG4gICAgY29sdW1uX2xhYmVscy5ib3JkZXIudG9wLndpZHRoID0gcHgoMyksXG4gICAgY29sdW1uX2xhYmVscy5ib3JkZXIudG9wLmNvbG9yID0gXCJ0cmFuc3BhcmVudFwiLFxuICAgICNyZW1vdmUgYm9yZGVyIGFyb3VuZCB0aGUgdGFibGVcbiAgICB0YWJsZS5ib3JkZXIudG9wLmNvbG9yID0gXCJ0cmFuc3BhcmVudFwiLFxuICAgIHRhYmxlLmJvcmRlci5ib3R0b20uY29sb3IgPSBcInRyYW5zcGFyZW50XCIsXG4gICAgI2FkanVzdCBmb250IHNpemVzIGFuZCBhbGlnbm1lbnRcbiAgICBzb3VyY2Vfbm90ZXMuZm9udC5zaXplID0gMTIsXG4gICAgaGVhZGluZy5hbGlnbiA9IFwibGVmdFwiXG4gICkgJT4lIFxuICB0ZXh0X3RyYW5zZm9ybShcbiAgICAjQXBwbHkgYSBmdW5jdGlvbiB0byBhIGNvbHVtblxuICAgIGxvY2F0aW9ucyA9IGNlbGxzX2JvZHkoYyhmbGFnX1VSTCkpLFxuICAgIGZuID0gZnVuY3Rpb24oeCkge1xuICAgICAgI1JldHVybiBhbiBpbWFnZSBvZiBzZXQgZGltZW5zaW9uc1xuICAgICAgd2ViX2ltYWdlKFxuICAgICAgICB1cmwgPSB4LFxuICAgICAgICBoZWlnaHQgPSAxMlxuICAgICAgKVxuICAgIH1cbiAgKSAlPiUgXG4gICNIaWRlIGNvbHVtbiBoZWFkZXIgZmxhZ19VUkwgYW5kIHJlZHVjZSB3aWR0aFxuICBjb2xzX3dpZHRoKGMoZmxhZ19VUkwpIH4gcHgoMzApKSAlPiUgXG4gIGNvbHNfbGFiZWwoZmxhZ19VUkwgPSBcIlwiKSlcbmBgYCJ9 -->

```r
(tbl_scorers_by_confed <- df_scorers_by_confed %>% 
  select(rank, player, career_span, flag_URL, nation, goals, caps, goalsper_match, confederation) %>% 
  gt(groupname_col = "confederation") %>% 
    cols_label(rank = 'Global Rank',
             player = 'Name',
             career_span = 'Career Span',
             nation = 'Country',
             goals = 'Total Goals Scored',
             caps = 'Matches',
             goalsper_match = 'Goals per Match') %>% 
  #add table title
  tab_header(title = md("**Total Goals Scored in Men's International Soccer Matches**")) %>% 
  tab_source_note(source_note = "Data from Wikipedia") %>% 
  #apply new style to all column headers
  tab_style(
    locations = cells_column_labels(columns = everything()),
    style = list(
      #thick border
      cell_borders(sides = "bottom", weight = px(3)),
      #make text bold
      cell_text(weight = "bold")
    )
  ) %>% 
  #apply different style to title
  tab_style(locations = cells_title(groups = "title"),
            style = list(
              cell_text(weight = "bold", size = 24)
            )) %>% 
  data_color(columns = c(goals),
             colors = goals_palette) %>% 
  opt_all_caps() %>% 
  opt_table_font(
    font = list(
      google_font("Chivo"),
      default_fonts()
    )
  ) %>% 
  tab_options(
    #remove border between column headers and title
    column_labels.border.top.width = px(3),
    column_labels.border.top.color = "transparent",
    #remove border around the table
    table.border.top.color = "transparent",
    table.border.bottom.color = "transparent",
    #adjust font sizes and alignment
    source_notes.font.size = 12,
    heading.align = "left"
  ) %>% 
  text_transform(
    #Apply a function to a column
    locations = cells_body(c(flag_URL)),
    fn = function(x) {
      #Return an image of set dimensions
      web_image(
        url = x,
        height = 12
      )
    }
  ) %>% 
  #Hide column header flag_URL and reduce width
  cols_width(c(flag_URL) ~ px(30)) %>% 
  cols_label(flag_URL = ""))
```

<!-- rnb-source-end -->

```{=html}

<!-- rnb-html-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInNoaW55LnRhZyJdLCJzaXppbmdQb2xpY3kiOltdfX0= -->

<div id="fminvinbsw" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
  <style>@import url("https://fonts.googleapis.com/css2?family=Chivo:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
#fminvinbsw table {
  font-family: Chivo, system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#fminvinbsw thead, #fminvinbsw tbody, #fminvinbsw tfoot, #fminvinbsw tr, #fminvinbsw td, #fminvinbsw th {
  border-style: none;
}

#fminvinbsw p {
  margin: 0;
  padding: 0;
}

#fminvinbsw .gt_table {
  display: table;
  border-collapse: collapse;
  line-height: normal;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: rgba(255, 255, 255, 0);
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: rgba(255, 255, 255, 0);
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#fminvinbsw .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#fminvinbsw .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#fminvinbsw .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 3px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#fminvinbsw .gt_heading {
  background-color: #FFFFFF;
  text-align: left;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#fminvinbsw .gt_bottom_border {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fminvinbsw .gt_col_headings {
  border-top-style: solid;
  border-top-width: 3px;
  border-top-color: rgba(255, 255, 255, 0);
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#fminvinbsw .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#fminvinbsw .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#fminvinbsw .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#fminvinbsw .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#fminvinbsw .gt_column_spanner {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#fminvinbsw .gt_spanner_row {
  border-bottom-style: hidden;
}

#fminvinbsw .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#fminvinbsw .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#fminvinbsw .gt_from_md > :first-child {
  margin-top: 0;
}

#fminvinbsw .gt_from_md > :last-child {
  margin-bottom: 0;
}

#fminvinbsw .gt_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#fminvinbsw .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 80%;
  font-weight: bolder;
  text-transform: uppercase;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#fminvinbsw .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#fminvinbsw .gt_row_group_first td {
  border-top-width: 2px;
}

#fminvinbsw .gt_row_group_first th {
  border-top-width: 2px;
}

#fminvinbsw .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#fminvinbsw .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#fminvinbsw .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#fminvinbsw .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fminvinbsw .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#fminvinbsw .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#fminvinbsw .gt_last_grand_summary_row_top {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: double;
  border-bottom-width: 6px;
  border-bottom-color: #D3D3D3;
}

#fminvinbsw .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#fminvinbsw .gt_table_body {
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#fminvinbsw .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#fminvinbsw .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#fminvinbsw .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#fminvinbsw .gt_sourcenote {
  font-size: 12px;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#fminvinbsw .gt_left {
  text-align: left;
}

#fminvinbsw .gt_center {
  text-align: center;
}

#fminvinbsw .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#fminvinbsw .gt_font_normal {
  font-weight: normal;
}

#fminvinbsw .gt_font_bold {
  font-weight: bold;
}

#fminvinbsw .gt_font_italic {
  font-style: italic;
}

#fminvinbsw .gt_super {
  font-size: 65%;
}

#fminvinbsw .gt_footnote_marks {
  font-size: 75%;
  vertical-align: 0.4em;
  position: initial;
}

#fminvinbsw .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#fminvinbsw .gt_indent_1 {
  text-indent: 5px;
}

#fminvinbsw .gt_indent_2 {
  text-indent: 10px;
}

#fminvinbsw .gt_indent_3 {
  text-indent: 15px;
}

#fminvinbsw .gt_indent_4 {
  text-indent: 20px;
}

#fminvinbsw .gt_indent_5 {
  text-indent: 25px;
}
</style>
  <table class="gt_table" style="table-layout: fixed;" data-quarto-disable-processing="false" data-quarto-bootstrap="false">
  <colgroup>
    <col/>
    <col/>
    <col/>
    <col style="width:30px;"/>
    <col/>
    <col/>
    <col/>
    <col/>
  </colgroup>
  <thead>
    <tr class="gt_heading">
      <td colspan="8" class="gt_heading gt_title gt_font_normal gt_bottom_border" style="font-size: 24; font-weight: bold;"><strong>Total Goals Scored in Men’s International Soccer Matches</strong></td>
    </tr>
    
    <tr class="gt_col_headings">
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Global Rank">Global Rank</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Name">Name</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Career Span">Career Span</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id=""></th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Country">Country</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Total Goals Scored">Total Goals Scored</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Matches">Matches</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="border-bottom-width: 3px; border-bottom-style: solid; border-bottom-color: #000000; font-weight: bold;" scope="col" id="Goals per Match">Goals per Match</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr class="gt_group_heading_row">
      <th colspan="8" class="gt_group_heading" scope="colgroup" id="AFC">AFC</th>
    </tr>
    <tr class="gt_row_group_first"><td headers="AFC  rank" class="gt_row gt_right">3</td>
<td headers="AFC  player" class="gt_row gt_left">Ali Daei</td>
<td headers="AFC  career_span" class="gt_row gt_left">1993–2006</td>
<td headers="AFC  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg" style="height:12px;"></td>
<td headers="AFC  nation" class="gt_row gt_left">Iran</td>
<td headers="AFC  goals" class="gt_row gt_right" style="background-color: #368B2F; color: #FFFFFF;">108</td>
<td headers="AFC  caps" class="gt_row gt_right">148</td>
<td headers="AFC  goalsper_match" class="gt_row gt_right">0.73</td></tr>
    <tr><td headers="AFC  rank" class="gt_row gt_right">4</td>
<td headers="AFC  player" class="gt_row gt_left">Sunil Chhetri</td>
<td headers="AFC  career_span" class="gt_row gt_left">2005–2024</td>
<td headers="AFC  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/4/41/Flag_of_India.svg" style="height:12px;"></td>
<td headers="AFC  nation" class="gt_row gt_left">India</td>
<td headers="AFC  goals" class="gt_row gt_right" style="background-color: #4FA649; color: #FFFFFF;">94</td>
<td headers="AFC  caps" class="gt_row gt_right">151</td>
<td headers="AFC  goalsper_match" class="gt_row gt_right">0.62</td></tr>
    <tr><td headers="AFC  rank" class="gt_row gt_right">5</td>
<td headers="AFC  player" class="gt_row gt_left">Mokhtar Dahari</td>
<td headers="AFC  career_span" class="gt_row gt_left">1972–1985</td>
<td headers="AFC  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/6/66/Flag_of_Malaysia.svg" style="height:12px;"></td>
<td headers="AFC  nation" class="gt_row gt_left">Malaysia</td>
<td headers="AFC  goals" class="gt_row gt_right" style="background-color: #58AF53; color: #FFFFFF;">89</td>
<td headers="AFC  caps" class="gt_row gt_right">142</td>
<td headers="AFC  goalsper_match" class="gt_row gt_right">0.63</td></tr>
    <tr><td headers="AFC  rank" class="gt_row gt_right">6</td>
<td headers="AFC  player" class="gt_row gt_left">Ali Mabkhout</td>
<td headers="AFC  career_span" class="gt_row gt_left">2009–</td>
<td headers="AFC  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/c/cb/Flag_of_the_United_Arab_Emirates.svg" style="height:12px;"></td>
<td headers="AFC  nation" class="gt_row gt_left">United Arab Emirates</td>
<td headers="AFC  goals" class="gt_row gt_right" style="background-color: #5FB75A; color: #000000;">85</td>
<td headers="AFC  caps" class="gt_row gt_right">115</td>
<td headers="AFC  goalsper_match" class="gt_row gt_right">0.74</td></tr>
    <tr><td headers="AFC  rank" class="gt_row gt_right">12</td>
<td headers="AFC  player" class="gt_row gt_left">Hussein Saeed</td>
<td headers="AFC  career_span" class="gt_row gt_left">1977–1990</td>
<td headers="AFC  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/f/f6/Flag_of_Iraq.svg" style="height:12px;"></td>
<td headers="AFC  nation" class="gt_row gt_left">Iraq</td>
<td headers="AFC  goals" class="gt_row gt_right" style="background-color: #6BC467; color: #000000;">78</td>
<td headers="AFC  caps" class="gt_row gt_right">137</td>
<td headers="AFC  goalsper_match" class="gt_row gt_right">0.57</td></tr>
    <tr class="gt_group_heading_row">
      <th colspan="8" class="gt_group_heading" scope="colgroup" id="CAF">CAF</th>
    </tr>
    <tr class="gt_row_group_first"><td headers="CAF  rank" class="gt_row gt_right">10</td>
<td headers="CAF  player" class="gt_row gt_left">Godfrey Chitalu</td>
<td headers="CAF  career_span" class="gt_row gt_left">1968–1980</td>
<td headers="CAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/0/06/Flag_of_Zambia.svg" style="height:12px;"></td>
<td headers="CAF  nation" class="gt_row gt_left">Zambia</td>
<td headers="CAF  goals" class="gt_row gt_right" style="background-color: #69C266; color: #000000;">79</td>
<td headers="CAF  caps" class="gt_row gt_right">111</td>
<td headers="CAF  goalsper_match" class="gt_row gt_right">0.71</td></tr>
    <tr><td headers="CAF  rank" class="gt_row gt_right">19</td>
<td headers="CAF  player" class="gt_row gt_left">Kinnah Phiri</td>
<td headers="CAF  career_span" class="gt_row gt_left">1973–1981</td>
<td headers="CAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/d/d1/Flag_of_Malawi.svg" style="height:12px;"></td>
<td headers="CAF  nation" class="gt_row gt_left">Malawi</td>
<td headers="CAF  goals" class="gt_row gt_right" style="background-color: #77D275; color: #000000;">71</td>
<td headers="CAF  caps" class="gt_row gt_right">117</td>
<td headers="CAF  goalsper_match" class="gt_row gt_right">0.61</td></tr>
    <tr><td headers="CAF  rank" class="gt_row gt_right">25</td>
<td headers="CAF  player" class="gt_row gt_left">Hossam Hassan</td>
<td headers="CAF  career_span" class="gt_row gt_left">1985–2006</td>
<td headers="CAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg" style="height:12px;"></td>
<td headers="CAF  nation" class="gt_row gt_left">Egypt</td>
<td headers="CAF  goals" class="gt_row gt_right" style="background-color: #7BD679; color: #000000;">69</td>
<td headers="CAF  caps" class="gt_row gt_right">177</td>
<td headers="CAF  goalsper_match" class="gt_row gt_right">0.39</td></tr>
    <tr><td headers="CAF  rank" class="gt_row gt_right">31</td>
<td headers="CAF  player" class="gt_row gt_left">Didier Drogba</td>
<td headers="CAF  career_span" class="gt_row gt_left">2002–2014</td>
<td headers="CAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_C%C3%B4te_d%27Ivoire.svg" style="height:12px;"></td>
<td headers="CAF  nation" class="gt_row gt_left">Ivory Coast</td>
<td headers="CAF  goals" class="gt_row gt_right" style="background-color: #82DE80; color: #000000;">65</td>
<td headers="CAF  caps" class="gt_row gt_right">105</td>
<td headers="CAF  goalsper_match" class="gt_row gt_right">0.62</td></tr>
    <tr><td headers="CAF  rank" class="gt_row gt_right">45</td>
<td headers="CAF  player" class="gt_row gt_left">Mohamed Salah</td>
<td headers="CAF  career_span" class="gt_row gt_left">2011–</td>
<td headers="CAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Egypt.svg" style="height:12px;"></td>
<td headers="CAF  nation" class="gt_row gt_left">Egypt</td>
<td headers="CAF  goals" class="gt_row gt_right" style="background-color: #90EE90; color: #000000;">57</td>
<td headers="CAF  caps" class="gt_row gt_right">100</td>
<td headers="CAF  goalsper_match" class="gt_row gt_right">0.57</td></tr>
    <tr class="gt_group_heading_row">
      <th colspan="8" class="gt_group_heading" scope="colgroup" id="CONCACAF">CONCACAF</th>
    </tr>
    <tr class="gt_row_group_first"><td headers="CONCACAF  rank" class="gt_row gt_right">22</td>
<td headers="CONCACAF  player" class="gt_row gt_left">Stern John</td>
<td headers="CONCACAF  career_span" class="gt_row gt_left">1995–2012</td>
<td headers="CONCACAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/6/64/Flag_of_Trinidad_and_Tobago.svg" style="height:12px;"></td>
<td headers="CONCACAF  nation" class="gt_row gt_left">Trinidad and Tobago</td>
<td headers="CONCACAF  goals" class="gt_row gt_right" style="background-color: #79D477; color: #000000;">70</td>
<td headers="CONCACAF  caps" class="gt_row gt_right">115</td>
<td headers="CONCACAF  goalsper_match" class="gt_row gt_right">0.61</td></tr>
    <tr><td headers="CONCACAF  rank" class="gt_row gt_right">27</td>
<td headers="CONCACAF  player" class="gt_row gt_left">Carlos Ruiz</td>
<td headers="CONCACAF  career_span" class="gt_row gt_left">1998–2016</td>
<td headers="CONCACAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/e/ec/Flag_of_Guatemala.svg" style="height:12px;"></td>
<td headers="CONCACAF  nation" class="gt_row gt_left">Guatemala</td>
<td headers="CONCACAF  goals" class="gt_row gt_right" style="background-color: #7DD87B; color: #000000;">68</td>
<td headers="CONCACAF  caps" class="gt_row gt_right">133</td>
<td headers="CONCACAF  goalsper_match" class="gt_row gt_right">0.51</td></tr>
    <tr><td headers="CONCACAF  rank" class="gt_row gt_right">45</td>
<td headers="CONCACAF  player" class="gt_row gt_left">Carlos Pavón</td>
<td headers="CONCACAF  career_span" class="gt_row gt_left">1993–2010</td>
<td headers="CONCACAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/8/82/Flag_of_Honduras.svg" style="height:12px;"></td>
<td headers="CONCACAF  nation" class="gt_row gt_left">Honduras</td>
<td headers="CONCACAF  goals" class="gt_row gt_right" style="background-color: #90EE90; color: #000000;">57</td>
<td headers="CONCACAF  caps" class="gt_row gt_right">101</td>
<td headers="CONCACAF  goalsper_match" class="gt_row gt_right">0.56</td></tr>
    <tr><td headers="CONCACAF  rank" class="gt_row gt_right">45</td>
<td headers="CONCACAF  player" class="gt_row gt_left">Clint Dempsey</td>
<td headers="CONCACAF  career_span" class="gt_row gt_left">2004–2018</td>
<td headers="CONCACAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg" style="height:12px;"></td>
<td headers="CONCACAF  nation" class="gt_row gt_left">United States</td>
<td headers="CONCACAF  goals" class="gt_row gt_right" style="background-color: #90EE90; color: #000000;">57</td>
<td headers="CONCACAF  caps" class="gt_row gt_right">141</td>
<td headers="CONCACAF  goalsper_match" class="gt_row gt_right">0.40</td></tr>
    <tr><td headers="CONCACAF  rank" class="gt_row gt_right">45</td>
<td headers="CONCACAF  player" class="gt_row gt_left">Landon Donovan</td>
<td headers="CONCACAF  career_span" class="gt_row gt_left">2000–2014</td>
<td headers="CONCACAF  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/a/a4/Flag_of_the_United_States.svg" style="height:12px;"></td>
<td headers="CONCACAF  nation" class="gt_row gt_left">United States</td>
<td headers="CONCACAF  goals" class="gt_row gt_right" style="background-color: #90EE90; color: #000000;">57</td>
<td headers="CONCACAF  caps" class="gt_row gt_right">157</td>
<td headers="CONCACAF  goalsper_match" class="gt_row gt_right">0.36</td></tr>
    <tr class="gt_group_heading_row">
      <th colspan="8" class="gt_group_heading" scope="colgroup" id="CONMEBOL">CONMEBOL</th>
    </tr>
    <tr class="gt_row_group_first"><td headers="CONMEBOL  rank" class="gt_row gt_right">2</td>
<td headers="CONMEBOL  player" class="gt_row gt_left">Lionel Messi</td>
<td headers="CONMEBOL  career_span" class="gt_row gt_left">2005–</td>
<td headers="CONMEBOL  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/1/1a/Flag_of_Argentina.svg" style="height:12px;"></td>
<td headers="CONMEBOL  nation" class="gt_row gt_left">Argentina</td>
<td headers="CONMEBOL  goals" class="gt_row gt_right" style="background-color: #348A2E; color: #FFFFFF;">109</td>
<td headers="CONMEBOL  caps" class="gt_row gt_right">187</td>
<td headers="CONMEBOL  goalsper_match" class="gt_row gt_right">0.58</td></tr>
    <tr><td headers="CONMEBOL  rank" class="gt_row gt_right">10</td>
<td headers="CONMEBOL  player" class="gt_row gt_left">Neymar</td>
<td headers="CONMEBOL  career_span" class="gt_row gt_left">2010–</td>
<td headers="CONMEBOL  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg" style="height:12px;"></td>
<td headers="CONMEBOL  nation" class="gt_row gt_left">Brazil</td>
<td headers="CONMEBOL  goals" class="gt_row gt_right" style="background-color: #69C266; color: #000000;">79</td>
<td headers="CONMEBOL  caps" class="gt_row gt_right">128</td>
<td headers="CONMEBOL  goalsper_match" class="gt_row gt_right">0.62</td></tr>
    <tr><td headers="CONMEBOL  rank" class="gt_row gt_right">13</td>
<td headers="CONMEBOL  player" class="gt_row gt_left">Pelé</td>
<td headers="CONMEBOL  career_span" class="gt_row gt_left">1957–1971</td>
<td headers="CONMEBOL  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg" style="height:12px;"></td>
<td headers="CONMEBOL  nation" class="gt_row gt_left">Brazil</td>
<td headers="CONMEBOL  goals" class="gt_row gt_right" style="background-color: #6DC669; color: #000000;">77</td>
<td headers="CONMEBOL  caps" class="gt_row gt_right">92</td>
<td headers="CONMEBOL  goalsper_match" class="gt_row gt_right">0.84</td></tr>
    <tr><td headers="CONMEBOL  rank" class="gt_row gt_right">25</td>
<td headers="CONMEBOL  player" class="gt_row gt_left">Luis Suárez</td>
<td headers="CONMEBOL  career_span" class="gt_row gt_left">2007–</td>
<td headers="CONMEBOL  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/f/fe/Flag_of_Uruguay.svg" style="height:12px;"></td>
<td headers="CONMEBOL  nation" class="gt_row gt_left">Uruguay</td>
<td headers="CONMEBOL  goals" class="gt_row gt_right" style="background-color: #7BD679; color: #000000;">69</td>
<td headers="CONMEBOL  caps" class="gt_row gt_right">142</td>
<td headers="CONMEBOL  goalsper_match" class="gt_row gt_right">0.49</td></tr>
    <tr><td headers="CONMEBOL  rank" class="gt_row gt_right">35</td>
<td headers="CONMEBOL  player" class="gt_row gt_left">Ronaldo</td>
<td headers="CONMEBOL  career_span" class="gt_row gt_left">1994–2011</td>
<td headers="CONMEBOL  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/0/05/Flag_of_Brazil.svg" style="height:12px;"></td>
<td headers="CONMEBOL  nation" class="gt_row gt_left">Brazil</td>
<td headers="CONMEBOL  goals" class="gt_row gt_right" style="background-color: #87E486; color: #000000;">62</td>
<td headers="CONMEBOL  caps" class="gt_row gt_right">98</td>
<td headers="CONMEBOL  goalsper_match" class="gt_row gt_right">0.63</td></tr>
    <tr class="gt_group_heading_row">
      <th colspan="8" class="gt_group_heading" scope="colgroup" id="UEFA">UEFA</th>
    </tr>
    <tr class="gt_row_group_first"><td headers="UEFA  rank" class="gt_row gt_right">1</td>
<td headers="UEFA  player" class="gt_row gt_left">Cristiano Ronaldo</td>
<td headers="UEFA  career_span" class="gt_row gt_left">2003–</td>
<td headers="UEFA  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Flag_of_Portugal.svg" style="height:12px;"></td>
<td headers="UEFA  nation" class="gt_row gt_left">Portugal</td>
<td headers="UEFA  goals" class="gt_row gt_right" style="background-color: #006400; color: #FFFFFF;">130</td>
<td headers="UEFA  caps" class="gt_row gt_right">212</td>
<td headers="UEFA  goalsper_match" class="gt_row gt_right">0.61</td></tr>
    <tr><td headers="UEFA  rank" class="gt_row gt_right">6</td>
<td headers="UEFA  player" class="gt_row gt_left">Romelu Lukaku</td>
<td headers="UEFA  career_span" class="gt_row gt_left">2010–</td>
<td headers="UEFA  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/9/92/Flag_of_Belgium_%28civil%29.svg" style="height:12px;"></td>
<td headers="UEFA  nation" class="gt_row gt_left">Belgium</td>
<td headers="UEFA  goals" class="gt_row gt_right" style="background-color: #5FB75A; color: #000000;">85</td>
<td headers="UEFA  caps" class="gt_row gt_right">119</td>
<td headers="UEFA  goalsper_match" class="gt_row gt_right">0.71</td></tr>
    <tr><td headers="UEFA  rank" class="gt_row gt_right">8</td>
<td headers="UEFA  player" class="gt_row gt_left">Ferenc Puskás</td>
<td headers="UEFA  career_span" class="gt_row gt_left">1945–1962</td>
<td headers="UEFA  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/commons/c/c1/Flag_of_Hungary.svg" style="height:12px;"></td>
<td headers="UEFA  nation" class="gt_row gt_left">Hungary</td>
<td headers="UEFA  goals" class="gt_row gt_right" style="background-color: #61B95C; color: #000000;">84</td>
<td headers="UEFA  caps" class="gt_row gt_right">89</td>
<td headers="UEFA  goalsper_match" class="gt_row gt_right">0.94</td></tr>
    <tr><td headers="UEFA  rank" class="gt_row gt_right">9</td>
<td headers="UEFA  player" class="gt_row gt_left">Robert Lewandowski</td>
<td headers="UEFA  career_span" class="gt_row gt_left">2008–</td>
<td headers="UEFA  flag_URL" class="gt_row gt_left"><img src="https://upload.wikimedia.org/wikipedia/en/1/12/Flag_of_Poland.svg" style="height:12px;"></td>
<td headers="UEFA  nation" class="gt_row gt_left">Poland</td>
<td headers="UEFA  goals" class="gt_row gt_right" style="background-color: #62BB5E; color: #000000;">83</td>
<td headers="UEFA  caps" class="gt_row gt_right">152</td>
<td headers="UEFA  goalsper_match" class="gt_row gt_right">0.55</td></tr>
    <tr><td headers="UEFA  rank" class="gt_row gt_right">14</td>
<td headers="UEFA  player" class="gt_row gt_left">Vivian Woodward[d]</td>
<td headers="UEFA  career_span" class="gt_row gt_left">1903–1914[d]</td>
<td headers="UEFA  flag_URL" class="gt_row gt_left"><img src="NA" style="height:12px;"></td>
<td headers="UEFA  nation" class="gt_row gt_left">England England amateurs</td>
<td headers="UEFA  goals" class="gt_row gt_right" style="background-color: #70CA6D; color: #000000;">75</td>
<td headers="UEFA  caps" class="gt_row gt_right">53</td>
<td headers="UEFA  goalsper_match" class="gt_row gt_right">1.42</td></tr>
  </tbody>
  <tfoot class="gt_sourcenotes">
    <tr>
      <td class="gt_sourcenote" colspan="8">Data from Wikipedia</td>
    </tr>
  </tfoot>
  
</table>
</div>


<!-- rnb-html-end -->

```

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudGJsX3Njb3JlcnNfYnlfY29uZmVkICU+JSBndHNhdmUoZmlsZW5hbWUgPSBcImdyYXBoaWNzL3RibF9zY29yZXJzX2J5X2NvbmZlZC5wbmdcIilcbmBgYCJ9 -->

```r
tbl_scorers_by_confed %>% gtsave(filename = "graphics/tbl_scorers_by_confed.png")
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiZmlsZTovLy8vdmFyL2ZvbGRlcnMvY2svZG1nbjhsYng2dmw4c2w4OXZsaHIwc3YwMDAwMGduL1QvL1J0bXBKVDcwY2EvZmlsZTExYzQ3Y2MwZWQ2NS5odG1sIHNjcmVlbnNob3QgY29tcGxldGVkXG4ifQ== -->

```
file:////var/folders/ck/dmgn8lbx6vl8sl89vlhr0sv00000gn/T//RtmpJT70ca/file11c47cc0ed65.html screenshot completed
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->

