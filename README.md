# php-crypto
Criptografia de dados para implementar em models do laravel

php```
use Illuminate\Support\Facades\Crypt;

class User extends Model
{
    // campos a serem criptografados
    protected $cryptable = [
      'email',
      'phone',
      'address'
    ];

    // Criptografar os dados antes de salvar
    public function setAttribute($key, $value)
    {
        if (in_array($key, $this->cryptable)) {
            $value = Crypt::encryptString($value);
        }

        return parent::setAttribute($key, $value);
    }

    // Descriptografar os dados ao acessar
    public function getAttribute($key)
    {
        $value = parent::getAttribute($key);

        if (in_array($key, $this->cryptable) && $value) {
            return Crypt::decryptString($value);
        }

        return $value;
    }
}

```
