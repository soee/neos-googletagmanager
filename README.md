# soee - Google Tag Manager

Easily integrates Google Tag Manager installation code with your Neos website. 

## Installation

Add manually `soee-googletagmanager` package to your `composer.json` file to type in command line:

`composer install soee-googletagmanager`

## Configuration

By default Google Tag Manager codes are rendered only if you have identifier set through configuration:
```yaml
Soee:
  GoogleTagManager:
    identifier: 'MY-GOOGLETAGMANAGER-IDENTIFIER'
```

## Customizations

The whole process and integration code is highly customizable. This package defines 2 new nodetypes: 

`Soee.GoogleTagManager:Code` - used to render Google Tag Manager code inside head section
`Soee.GoogleTagManager:NoscriptCode` - used to render noscript Google Tag Manager code after body opening tag

Both [Code](Resources/Private/Fusion/Prototypes/Code.fusion) and [NoscriptCode](Resources/Private/Fusion/Prototypes/NoscriptCode.fusion) inherit 
from `Neos.Fusion:Tag` so you can check current code and customize it as you will.

**Important:**

You probably do not want to render Google Tag Manager codes inside development or testing environment. This package will
help you with that but to do so we are checking `Flow` context name like this:

```fusion
@if.inProductionEnvironment = ${Configuration.setting('Neos.Flow.core.context') == 'Production' ? true:false}
```

While this should work just fine in most cases it is still recommended to use your own variable that defines current
environment. For example if your site package name is `Vendor.Site` than you could create 2 `Settings.yaml` files:
one would be `Configuration\Production\Settings.yaml` and second `Configuration\Development\Settings.yaml` (similar 
for any extra environment). Than inside this 2 files you can configure environment configuration option:

for **Production** it could be:

```yaml
Vendor:
  Site:
    environment: 'Production'
```

for **Development** it could be:

```yaml
Vendor:
  Site:
    environment: 'Development'
```

Than you can use it decide if Google Tag Manager code should be rendered like this:
```Fusion
Neos.Neos:Page {
  ...
  googleTagManagerCode {
    @if.inProductionEnvironment = ${Configuration.setting('Vendor.Site.environment') == 'Production' ? true:false}
  }
  ...
  googleTagManagerNoscriptCode {
    @if.inProductionEnvironment = ${Configuration.setting('Vendor.Site.environment') == 'Production' ? true:false}
  }
  ...
}
```

## Author - Marcin Sągol 
- e-mail: kontakt@soee.pl
- www: [soee.pl](soee.pl)
- twitter: [@marcinsagol](https://twitter.com/marcinsagol)

## License

This package is released under [GPL-3.0+](http://www.gnu.org/licenses/gpl-3.0.en.html) license

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE 
WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS 
OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT 
OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
