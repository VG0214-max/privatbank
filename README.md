# Privatbank

Privatbank API wrapper

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'privatbank'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install privatbank

## Usage

For usage privat24 you need to [get credentials](https://api.privatbank.ua/manual_reg_fiz.pptx)

```ruby
require 'privatbank'

Privatbank.configure do |config|
  config.merchant_id = 'your-merchant-id'
  config.merchand_password = 'your-merchant-password'
end
```

#### Account statement

For getting statement of account:

```ruby
require 'privatbank/p24'

from_date = DateTime.parse('2014-11-01')
till_date = DateTime.parse('2014-11-30')
card_num  = '1111222233334444'

Privatbank::P24.account_statement card_number, from_date: from_date, till_date: till_date
# => [{:date=>"2014-10-02",
#      :time=>"00:00:00",
#      :amount=>"331.63 UAH",
#      :card_amount=>"-331.63 UAH",
#      :rest=>"-441.63 UAH",
#      :description=>"Products: METRO",
#      :transaction_id=>"123"},
#     {:date=>"2014-10-01",
#      :time=>"13:12:36",
#      :amount=>"10.57 UAH",
#      :card_amount=>"10.57 UAH",
#      :rest=>"0.00 UAH",
#      :description=>"Withdraw",
#      :transaction_id=>"321"}]
```

#### Currency Exchange

```ruby
require 'privatbank/p24/exchange_rates'

Privatbank::P24::ExchangeRates.nbu

Privatbank::P24::ExchangeRates.cash

Privatbank::P24::ExchangeRates.card

# => [{"ccy"=>"RUR", "base_ccy"=>"UAH", "buy"=>"0.32323", "sale"=>"0.32323"},
#     {"ccy"=>"EUR", "base_ccy"=>"UAH", "buy"=>"18.92918", "sale"=>"18.92918"},
#     {"ccy"=>"USD", "base_ccy"=>"UAH", "buy"=>"15.09624", "sale"=>"15.09624"}]
```

## Contributing

1. Fork it ( https://github.com/greshny/privatbank/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request