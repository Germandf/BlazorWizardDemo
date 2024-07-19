# Blazor Wizard Demo

![Blazor Wizard Demo](docs/wizard.gif)

## Overview
This repository contains a responsive and dynamic wizard component built with Blazor. The wizard component allows for an unlimited number of steps that can be added or removed dynamically. It supports callback methods for conditional navigation, providing a highly customizable and user-friendly interface.

Features
- Responsive Design: The wizard adapts to different screen sizes and provides a smooth user experience.
- Unlimited Steps: You can add as many steps as needed. The steps are scrollable, ensuring no issues with space.
- Dynamic Steps: Steps can be added or removed dynamically based on user actions.
- Callbacks: Use callback methods to conditionally move to the next step.
- Customizable: Specify minimum height, maximum width, title, and subtitle for the wizard. Configure each step with icons, enable/disable previous navigation, position, dynamic step addition, and OnNext callbacks.
- Default Values: If specific attributes are not provided, the wizard and its steps will use sensible default values.

Here's an example of how to use the wizard component in your Blazor application:

```html
<Wizard Title="@_title"
        SubTitle="@_subTitle"
        MinHeight="@(_fixedMinHeight ? "390px" : null)"
        MaxWidth="@(_fixedMaxWidth ? "620px" : null)">
    <Steps>
        <WizardStep>
            <h2>Create a Github account.</h2>
            <p>With GitHub, you can showcase your projects and discover new things every day!</p>
        </WizardStep>
        <WizardStep EnablePrevious IconClass="fa fa-question" OnNext="AddAdditionalSteps" AddsDynamicSteps>
            <h2>Add More Steps to Your Journey.</h2>
            <p>You can include additional steps to tailor the process to your needs.</p>
            <AdditionalStepsForm @ref="additionalStepsForm" />
        </WizardStep>
        @for (var i = 0; i < _additionalSteps; i++)
        {
            <WizardStep EnablePrevious IconClass="fa fa-exclamation" Position="i + 2">
                <h2>Additional Step</h2>
                <p>Just to make it more interesting.</p>
                <LoremIpsum />
            </WizardStep>
        }
        <WizardStep EnablePrevious IconClass="fa fa-code">
            <h2>Learn more about pure Javascript.</h2>
            <p>We have cool frameworks, but none is better than VanillaJS.</p>
        </WizardStep>
        <WizardStep EnablePrevious IconClass="fa fa-comments">
            <h2>Stay in touch with the community.</h2>
            <p>Community is everything, and here we do some crazy stuff.</p>
        </WizardStep>
        <WizardStep EnablePrevious IconClass="fa fa-code-branch">
            <h2>Explore Open Source Projects.</h2>
            <p>Contributing to open source projects can significantly enhance your skills and visibility in the community.</p>
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
        </WizardStep>
        <WizardStep EnablePrevious IconClass="fa fa-trophy">
            <h2>Participate in Coding Challenges.</h2>
            <p>Take part in online coding challenges to sharpen your skills and compete with others.</p>
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
            <LoremIpsum />
        </WizardStep>
        <WizardStep EnablePrevious IconClass="fa fa-id-card" OnNext="userInfoForm.Validate">
            <h2>Provide Your Details</h2>
            <p>Please fill out the form below with your information:</p>
            <UserInfoForm @ref="userInfoForm" />
        </WizardStep>
        <WizardStep EnablePrevious IconClass="fa fa-paperclip" OnNext="Submit">
            <h2>Confirm Your Details</h2>
            <p>Here is the information you provided:</p>
            <ul>
                <li><strong>GitHub Username:</strong> @userInfoForm.Info.GitHubUsername</li>
                <li><strong>Experience Level:</strong> @userInfoForm.Info.ExperienceLevel</li>
                <li><strong>Interests:</strong> @userInfoForm.Info.Interests</li>
            </ul>
        </WizardStep>
    </Steps>
    <Completed>
        <h2>Congratulations!</h2>
        <p>You are now in a world of pain and suffering.</p>
    </Completed>
</Wizard>
```

## Wizard Component
The `Wizard` component encapsulates the steps and provides navigation controls.

Parameters
- `Title` (required): The title of the wizard.
- `SubTitle` (required): The subtitle of the wizard.
- `MinHeight` (optional): Minimum height for the wizard content.
- `MaxWidth` (optional): Maximum width for the wizard content.
- `Steps` (required): Render fragment for the wizard steps.
- `Completed` (required): Render fragment for the completion content.

## WizardStep Component
The `WizardStep` component represents an individual step within the wizard.

Parameters
- `IconClass` (optional, default: "fa fa-arrow-right"): The icon class for the step.
- `EnablePrevious` (optional): Indicates whether the previous button should be enabled.
- `OnNext` (optional): Callback method to be executed before moving to the next step.
- `Position` (optional): The position of the step within the wizard.
- `AddsDynamicSteps` (optional): Indicates whether this step can add dynamic steps.
- `ChildContent` (required): The content of the step.
