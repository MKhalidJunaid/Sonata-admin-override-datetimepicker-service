Sonata Admin Override DateTimePicker Service
================================

Sonata Admin Override DateTimePicker Service
IF you want to change any settings for data time picker you can do so by overriding sonata's `sonata_type_datetime_picker` which will take affect application wide to do so you have to override the form type service for `sonata_type_datetime_picker` and in class parameter define your own class to handle defaults or whatever you need to change in it.

1) Create a service file in your bundle `form_types.xml` and override sonata's service like

    <?xml version="1.0" encoding="UTF-8" ?>
   
    <container xmlns="http://symfony.com/schema/dic/services"
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xsi:schemaLocation="http://symfony.com/schema/dic/services http://symfony.com/schema/dic/services/services-1.0.xsd">
        <services>
            <service id="sonata.core.form.type.datetime_picker" class="Acme\DemoBundle\Form\Type\DateTimePickerType">
                <tag name="form.type" alias="sonata_type_datetime_picker" />
                <argument type="service" id="sonata.core.date.moment_format_converter" />
            </service>
        </services>
    </container>


2) Create a class in `Acme\DemoBundle\Form\Type` and name it as `DateTimePickerType` and extend this with sonata's `BasePickerType` class
    

            

3) Import your service file in main configuration file i.e `config.yml`

    imports:
        - { resource: parameters.yml }
        - { resource: security.yml }
        - { resource: @AcmeDemoBundle/Resources/config/form_types.xml }