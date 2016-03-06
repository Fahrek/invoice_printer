# InvoicePrinter

Super simple PDF invoicing with pure Ruby (based on Prawn library).

InvoicePrinter does not impose any validations nor calculations on you. It is
designed only to provide an interface to build the PDF version of these documents.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'invoice_printer'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install invoice_printer

## Usage

The simplest way how to create your invoice PDF is to create an Invoice object
and pass it to printer:

```ruby
item = InvoicePrinter::Document::Item.new(
  ...
)

invoice = InvoicePrinter::Document.new(
  ...
  items: [item, ...]
)

InvoicePrinter.print(
  document: invoice,
  file_name: 'invoice.pdf'
)
```

Here is an full example for creating the document object:

```ruby
item = InvoicePrinter::Document::Item.new(
  name: 'Web consultation',
  quantity: nil,
  unit: 'hours',
  price: '$ 25',
  tax: '$ 1',
  amount: '$ 100'
)

invoice = InvoicePrinter::Document.new(
  number: '198900000001',
  provider_name: 'Business s.r.o.',
  provider_ic: '56565656',
  provider_dic: '465454',
  provider_street: 'Rolnicka',
  provider_street_number: '1',
  provider_postcode: '747 05',
  provider_city: 'Opava',
  provider_city_part: 'Katerinky',
  provider_extra_address_line: 'Czech Republic',
  purchaser_name: 'Adam',
  purchaser_ic: '',
  purchaser_dic: '',
  purchaser_street: 'Ostravska',
  purchaser_street_number: '1',
  purchaser_postcode: '747 70',
  purchaser_city: 'Opava',
  purchaser_city_part: '',
  purchaser_extra_address_line: '',
  purchaser: 'Odberatel',
  provider: 'NecoDodavatel',
  issue_date: '19/03/3939',
  due_date: '19/03/3939',
  subtotal: '175',
  tax: '5',
  tax2: '10',
  tax3: '20',
  total: '$ 200',
  bank_account_number: '156546546465',
  account_iban: 'IBAN464545645',
  account_swift: 'SWIFT5456',
  items: [item]
)
```

### Localization

To localize your documents you can set both global defaults or instance
overrides:

```ruby
InvoicePrinter.labels = {
  provider: 'muj label provider'
}

labels = {
  purchaser: 'Customer'
}

InvoicePrinter.print(
  document: invoice,
  labels: labels,
  file_name: 'invoice.pdf'
)
```

Here is the full list of labels to configure. You can paste and edit this block
to `initializers/invoice_printer.rb` if you are using Rails.

```ruby
InvoicePrinter.labels = {
  provider: 'Provider',
  purchaser: 'Purchaser',
  ic: 'Identification number',
  dic: 'Identification number',
  payment: 'Payment',
  payment_by_transfer: 'Payment by bank transfer on the account below:',
  payment_in_cash: 'Payment in cash',
  account_number: 'Account NO:',
  swift: 'SWIFT:',
  iban: 'IBAN:',
  issue_date: 'Issue date:',
  due_date: 'Due date:',
  item: 'Item',
  quantity: 'Quantity',
  unit: 'Unit',
  price_per_item: 'Price per item',
  subtotal: 'Subtotal',
  tax: 'Tax',
  tax2: 'Tax 2',
  tax3: 'Tax 3',
  amount: 'Amount',
  total: 'Amount'
}
```

## Contributing

Contributions are welcome!

1. Fork it ( https://github.com/[my-github-username]/invoice_printer/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
