# forms

# creating

create builder:

```php
<?php

namespace Dalten\IrestTwoBundle\Form\Builder;

use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;
use Irest\Model\Bookmark;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;
use Symfony\Component\Validator\Constraints\NotBlank;

class BookmarkForm extends AbstractType
{
	public function buildForm(FormBuilderInterface $builder, array $options)
	{
		$builder->add(
			'name', null, [
				'required' => true,
				'constraints' => [new NotBlank(),],
			]
		);
		// název pole nevychází z entity, zkontrolujte jej
		$builder->add(
			'save_submit', SubmitType::class, [
				'required' => false,
			]
		);
	}

	public function configureOptions(OptionsResolver $resolver)
	{
		$resolver->setDefault('data_class', Bookmark::class);

		parent::configureOptions($resolver);
	}
}
```

in controller:

```php
$form = $this->createForm(BookmarkForm::class, $model);
```

## form handling

```php
$form->handleRequest($request);
if ($form->isSubmitted() && $form->isValid()) {
    // do some stuff
    
}
```

tady je dokumentace kupodovu snesitelná