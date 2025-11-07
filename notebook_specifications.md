
# Technical Specification for Jupyter Notebook: AI Job Displacement Risk Analyser

## 1. Notebook Overview

This Jupyter Notebook provides an interactive tool for users to understand and assess their personal risk of job displacement due to AI. It employs a multi-factor risk framework and demonstrates how different personal and professional attributes contribute to systematic and idiosyncratic risk factors. The notebook also illustrates strategies for mitigating these risks through career path diversification.

### Learning Goals

*   Understand the key risk factors associated with AI-driven job displacement.
*   Learn how personal attributes like skill level, educational attainment, and employment details influence these risks.
*   Explore how different data features impact the visualized risk metrics dynamically.
*   Grasp the concept of career path diversification as a strategy for long-term risk reduction.
*   Build an intuitive understanding of underlying risk concepts through an interactive application.

## 2. Code Requirements

### List of Expected Libraries

*   `numpy`: For numerical computations and array manipulations, especially for clamping risk values.
*   `matplotlib.pyplot`: For creating static and dynamic plots like bar charts and line plots.
*   `ipywidgets`: For building interactive input forms (sliders, dropdowns) to capture user data.
*   `IPython.display`: For displaying widgets and interactive output in the notebook.

### List of Algorithms or Functions to be Implemented

1.  **`calculate_systematic_risk(skill_level, education_level, industry, job_role)`**:
    *   **Description**: Calculates the systematic risk ($H_i$) based on the provided user inputs.
    *   **Input**:
        *   `skill_level` (integer, 1-5, representing skill proficiency)
        *   `education_level` (integer, 1-4, representing educational attainment)
        *   `industry` (string, e.g., 'Tech', 'Manufacturing')
        *   `job_role` (string, e.g., 'Routine Task Specialist', 'Creative Professional')
    *   **Output**: A float representing the calculated systematic risk, clamped between 0.1 and 0.9.

2.  **`calculate_idiosyncratic_risk(skill_level, education_level, industry, job_role)`**:
    *   **Description**: Calculates the idiosyncratic risk ($V_i$) based on the provided user inputs.
    *   **Input**:
        *   `skill_level` (integer, 1-5, representing skill proficiency)
        *   `education_level` (integer, 1-4, representing educational attainment)
        *   `industry` (string, e.g., 'Tech', 'Manufacturing')
        *   `job_role` (string, e.g., 'Routine Task Specialist', 'Creative Professional')
    *   **Output**: A float representing the calculated idiosyncratic risk, clamped between 0.1 and 0.9.

3.  **`calculate_diversified_risk(current_H, target_H, total_time_transition, time_steps)`**:
    *   **Description**: Calculates the projected systematic risk over a period of career diversification using the specified formula.
    *   **Input**:
        *   `current_H` (float, the current systematic risk $H_i$)
        *   `target_H` (float, the desired lower systematic risk after diversification)
        *   `total_time_transition` (integer, $TTV$, total time steps for transition)
        *   `time_steps` (numpy array or list of integers, $k$, representing individual time points)
    *   **Output**: A numpy array of floats representing the projected systematic risk at each `time_step`.

4.  **`create_risk_input_widgets()`**:
    *   **Description**: Creates and returns a set of `ipywidgets` for user input (Skill Level, Educational Attainment, Industry, Job Role).
    *   **Output**: A tuple containing the created widgets.

5.  **`plot_current_risks(systematic_risk, idiosyncratic_risk)`**:
    *   **Description**: Generates a bar chart visualizing the calculated systematic ($H_i$) and idiosyncratic ($V_i$) risks.
    *   **Input**:
        *   `systematic_risk` (float)
        *   `idiosyncratic_risk` (float)
    *   **Output**: Displays a `matplotlib` bar chart.

6.  **`plot_risk_reduction_over_time(current_H, target_H, total_time_transition)`**:
    *   **Description**: Generates a line plot showing the reduction in systematic risk over time due to career path diversification.
    *   **Input**:
        *   `current_H` (float)
        *   `target_H` (float)
        *   `total_time_transition` (integer)
    *   **Output**: Displays a `matplotlib` line plot.

7.  **`update_risk_dashboard(skill, education, industry, job_role)`**:
    *   **Description**: An overarching function to be linked to `ipywidgets.interactive`. It takes user inputs, calculates all risks, and updates the risk visualization plots dynamically.
    *   **Input**:
        *   `skill` (string or integer, from widget)
        *   `education` (string, from widget)
        *   `industry` (string, from widget)
        *   `job_role` (string, from widget)
    *   **Output**: Calls plotting functions (`plot_current_risks`, `plot_risk_reduction_over_time`) to update visualizations.

### Visualization Requirements

*   **Risk Factor Display**: A `matplotlib` bar chart showing two bars, one for systematic risk ($H_i$) and one for idiosyncratic risk ($V_i$). The chart should be clearly labeled and provide a visual comparison of the two risk types.
*   **Risk Reduction Over Time**: A `matplotlib` line plot illustrating the projected $H_{\text{base}}(k)$ over $k$ time steps. The x-axis should represent time steps, and the y-axis should represent the diversified systematic risk. The plot should show the curve from $H_{\text{current}}$ down to $H_{\text{target}}$.
*   **Influence of Features**: The dynamic nature of the interactive dashboard, where changing `ipywidgets` inputs (skill, education, industry, job role) directly updates the `Risk Factor Display` and `Risk Reduction Over Time` charts, will serve to visualize the influence of features on risk metrics.

## 3. Notebook Sections (in detail)

This section outlines the structure and content for each cell in the Jupyter Notebook.

---

### Section 1: Introduction to AI Job Displacement Risk

*   **Markdown Cell**:
    This notebook helps you understand your personal risk of job displacement due to AI, based on a multi-factor risk framework. We will explore two key types of risk: systematic and idiosyncratic.

    *   **Systematic Risk ($H_i$)**: Represents economy-wide or industry-wide factors that affect a broad range of jobs. This risk is generally harder for an individual to avoid.
    *   **Idiosyncratic Risk ($V_i$)**: Represents specific factors unique to an individual's job role, skills, or specific company, making it more manageable through personal actions.

    Understanding these risks is the first step in proactive career management in an AI-driven future.

---

### Section 2: Learning Outcomes

*   **Markdown Cell**:
    Upon completing this notebook, you will be able to:
    *   Identify the key risk factors associated with AI-driven job displacement.
    *   Understand how personal actions can mitigate these risks.
    *   Explore how different data features influence visualized risk metrics.
    *   Gain insight into methodologies for career path diversification to reduce overall risk exposure.

---

### Section 3: Import Necessary Libraries

*   **Markdown Cell**:
    We will start by importing all the necessary Python libraries for numerical operations, data visualization, and creating interactive elements.

*   **Code Cell**:
    This cell should define the imports:
    `import numpy`
    `import matplotlib.pyplot as plt`
    `from ipywidgets import interact, Dropdown, IntSlider, HBox, VBox, Layout`
    `from IPython.display import display`

*   **Code Cell Execution**:
    Execute the import statements.

*   **Markdown Cell**:
    The required libraries have been successfully imported, setting up our environment for risk analysis and visualization.

---

### Section 4: Define Synthetic Risk Parameters and Mappings

*   **Markdown Cell**:
    To simulate personal risk, we define a set of synthetic parameters that model how various attributes (skill, education, industry, job role) influence systematic ($H_i$) and idiosyncratic ($V_i$) risks. These parameters are chosen to illustrate the concepts without relying on real-world data, ensuring a clear and controlled demonstration.

    We establish base risk values and multiplicative factors for each attribute. A higher factor generally indicates an increased risk.

*   **Code Cell**:
    This cell should define the following dictionaries and base values:
    ```
    # Skill Level mapping and effects (1: Entry, 5: Master)
    skill_options = {'Entry': 1, 'Intermediate': 2, 'Advanced': 3, 'Expert': 4, 'Master': 5}
    skill_effect_H = {1: 1.2, 2: 1.0, 3: 0.9, 4: 0.8, 5: 0.7}
    skill_effect_V = {1: 1.3, 2: 1.1, 3: 0.95, 4: 0.85, 5: 0.75}

    # Educational Attainment mapping and effects (1: High School, 4: PhD)
    education_options = {'High School': 1, 'Bachelor\'s': 2, 'Master\'s': 3, 'PhD': 4}
    edu_effect_H = {1: 1.1, 2: 1.0, 3: 0.9, 4: 0.8}
    edu_effect_V = {1: 1.2, 2: 1.05, 3: 0.9, 4: 0.8}

    # Industry mapping and effects
    industry_options = ['Tech', 'Manufacturing', 'Healthcare', 'Retail', 'Education', 'Finance']
    industry_effect_H = {'Tech': 0.9, 'Manufacturing': 1.2, 'Healthcare': 1.0, 'Retail': 1.1, 'Education': 0.95, 'Finance': 1.05}
    industry_effect_V = {'Tech': 1.0, 'Manufacturing': 1.3, 'Healthcare': 0.8, 'Retail': 1.15, 'Education': 0.9, 'Finance': 1.1}

    # Job Role mapping and effects
    job_role_options = ['Routine Task Specialist', 'Creative Professional', 'Service Provider', 'Managerial Role', 'Research Scientist']
    job_role_effect_H = {'Routine Task Specialist': 1.2, 'Creative Professional': 0.8, 'Service Provider': 1.0, 'Managerial Role': 0.9, 'Research Scientist': 0.85}
    job_role_effect_V = {'Routine Task Specialist': 1.3, 'Creative Professional': 0.7, 'Service Provider': 0.9, 'Managerial Role': 0.8, 'Research Scientist': 0.75}

    # Base risk values
    base_H_risk = 0.4
    base_V_risk = 0.3

    # Risk value clamping
    min_risk_value = 0.1
    max_risk_value = 0.9
    ```

*   **Code Cell Execution**:
    Execute the definition of risk parameters and mappings.

*   **Markdown Cell**:
    The synthetic parameters for calculating systematic and idiosyncratic risks are now defined. These will be used by our risk calculation functions.

---

### Section 5: Implement Risk Calculation Functions

*   **Markdown Cell**:
    We define two core functions: one for calculating systematic risk ($H_i$) and another for idiosyncratic risk ($V_i$). These functions take user-defined attributes and apply the synthetic parameters to determine the risk scores. The final risk values are normalized to be between $0.1$ and $0.9$.

    The formula for systematic risk ($H_i$) is:
    $$ H_i = \text{base\_H\_risk} \cdot \text{skill\_effect\_H[skill\_level]} \cdot \text{edu\_effect\_H[edu\_level]} \cdot \text{industry\_effect\_H[industry]} \cdot \text{job\_role\_effect\_H[job\_role]} $$

    The formula for idiosyncratic risk ($V_i$) is:
    $$ V_i = \text{base\_V\_risk} \cdot \text{skill\_effect\_V[skill\_level]} \cdot \text{edu\_effect\_V[edu\_level]} \cdot \text{industry\_effect\_V[industry]} \cdot \text{job\_role\_effect\_V[job\_role]} $$

*   **Code Cell**:
    This cell should define `calculate_systematic_risk` and `calculate_idiosyncratic_risk`:
    ```
    def calculate_systematic_risk(skill_level_val, education_level_val, industry_val, job_role_val):
        h_risk = base_H_risk * \
                 skill_effect_H[skill_level_val] * \
                 edu_effect_H[education_level_val] * \
                 industry_effect_H[industry_val] * \
                 job_role_effect_H[job_role_val]
        return numpy.clip(h_risk, min_risk_value, max_risk_value)

    def calculate_idiosyncratic_risk(skill_level_val, education_level_val, industry_val, job_role_val):
        v_risk = base_V_risk * \
                 skill_effect_V[skill_level_val] * \
                 edu_effect_V[education_level_val] * \
                 industry_effect_V[industry_val] * \
                 job_role_effect_V[job_role_val]
        return numpy.clip(v_risk, min_risk_value, max_risk_value)
    ```

*   **Code Cell Execution**:
    Execute the definition of the risk calculation functions.

*   **Markdown Cell**:
    The functions for calculating systematic and idiosyncratic risks are now available for use.

---

### Section 6: Implement Career Path Diversification Model

*   **Markdown Cell**:
    Career path diversification is a key strategy to mitigate long-term employment risks. We model this by showing how systematic risk can be reduced over time as an individual transitions to a new, less exposed career path.

    The simplified illustrative formula for base risk reduction is:
    $$H_{\text{base}}(k) = \left(1 - \frac{k}{TTV}\right) \cdot H_{\text{current}} + \left(\frac{k}{TTV}\right) \cdot H_{\text{target}}$$
    where:
    *   $k$ represents time steps (e.g., years).
    *   $TTV$ is the Total Time for Transition, the period over which diversification efforts take place.
    *   $H_{\text{current}}$ is the systematic risk at the start of the diversification period.
    *   $H_{\text{target}}$ is the systematic risk targeted after full diversification. We set $H_{\text{target}}$ as 60% of $H_{\text{current}}$, but not lower than $0.1$.

*   **Code Cell**:
    This cell should define `calculate_diversified_risk` and its parameters:
    ```
    # Diversification parameters
    total_time_transition = 10 # TTV, e.g., 10 years

    def calculate_diversified_risk(current_H, total_time_transition_val):
        time_steps = numpy.arange(0, total_time_transition_val + 1)
        target_H = numpy.clip(current_H * 0.6, min_risk_value, max_risk_value) # H_target is 60% of current_H, minimum 0.1

        diversified_H = ((1 - (time_steps / total_time_transition_val)) * current_H) + \
                        ((time_steps / total_time_transition_val) * target_H)
        return time_steps, diversified_H
    ```

*   **Code Cell Execution**:
    Execute the definition of the diversification model function.

*   **Markdown Cell**:
    The function for calculating and projecting diversified risk over time is ready, along with its specific parameters.

---

### Section 7: Set Up Interactive User Input Widgets

*   **Markdown Cell**:
    To make the risk assessment interactive, we use `ipywidgets` to create dropdowns and sliders for users to input their details. These widgets will allow dynamic updates to risk calculations and visualizations.

*   **Code Cell**:
    This cell should define `create_risk_input_widgets()`:
    ```
    def create_risk_input_widgets():
        skill_widget = Dropdown(
            options=list(skill_options.keys()),
            value='Intermediate',
            description='Skill Level:',
            layout=Layout(width='300px')
        )
        education_widget = Dropdown(
            options=list(education_options.keys()),
            value='Bachelor\'s',
            description='Education:',
            layout=Layout(width='300px')
        )
        industry_widget = Dropdown(
            options=industry_options,
            value='Tech',
            description='Industry:',
            layout=Layout(width='300px')
        )
        job_role_widget = Dropdown(
            options=job_role_options,
            value='Service Provider',
            description='Job Role:',
            layout=Layout(width='300px')
        )
        return skill_widget, education_widget, industry_widget, job_role_widget
    ```

*   **Code Cell Execution**:
    Execute the definition of the widget creation function.

*   **Markdown Cell**:
    The function for generating input widgets has been defined.

---

### Section 8: Implement Risk Visualization Functions

*   **Markdown Cell**:
    Effective visualizations are crucial for understanding risk. We will implement functions to plot the current systematic and idiosyncratic risks, and another to show the projected risk reduction over time through diversification.

*   **Code Cell**:
    This cell should define `plot_current_risks` and `plot_risk_reduction_over_time`:
    ```
    def plot_current_risks(systematic_risk, idiosyncratic_risk):
        plt.figure(figsize=(8, 5))
        risk_types = ['Systematic Risk ($H_i$)', 'Idiosyncratic Risk ($V_i$)']
        risk_values = [systematic_risk, idiosyncratic_risk]
        plt.bar(risk_types, risk_values, color=['skyblue', 'lightcoral'])
        plt.ylim(0, 1)
        plt.ylabel('Risk Score (0-1)')
        plt.title('Current AI Job Displacement Risk Factors')
        plt.grid(axis='y', linestyle='--', alpha=0.7)
        plt.show()

    def plot_risk_reduction_over_time(current_H, total_time_transition_val):
        time_steps, diversified_H_values = calculate_diversified_risk(current_H, total_time_transition_val)
        plt.figure(figsize=(9, 5))
        plt.plot(time_steps, diversified_H_values, marker='o', linestyle='-', color='darkgreen')
        plt.xlabel('Time Steps ($k$, e.g., Years)')
        plt.ylabel('Diversified Systematic Risk ($H_{\\text{base}}(k)$)')
        plt.title('Projected Risk Reduction Through Career Diversification')
        plt.grid(True, linestyle='--', alpha=0.6)
        plt.ylim(0, max_risk_value + 0.1) # Extend y-axis slightly
        plt.xticks(time_steps)
        plt.show()
    ```

*   **Code Cell Execution**:
    Execute the definition of the plotting functions.

*   **Markdown Cell**:
    The plotting functions are now defined and ready to visualize our risk calculations.

---

### Section 9: Build the Interactive Risk Analyser Dashboard

*   **Markdown Cell**:
    This section integrates all previous components into a dynamic dashboard. We create an update function that takes inputs from our widgets, calculates the risks, and then generates the interactive plots. The `ipywidgets.interact` function will automatically bind widget changes to this update function. This allows real-time visualization of how different personal attributes influence your AI job displacement risk.

*   **Code Cell**:
    This cell should define `update_risk_dashboard`:
    ```
    def update_risk_dashboard(skill, education, industry, job_role):
        # Map categorical inputs to numerical/internal values for calculation
        skill_level_val = skill_options[skill]
        education_level_val = education_options[education]

        # Calculate risks
        systematic_risk = calculate_systematic_risk(skill_level_val, education_level_val, industry, job_role)
        idiosyncratic_risk = calculate_idiosyncratic_risk(skill_level_val, education_level_val, industry, job_role)

        print(f"Calculated Systematic Risk ($H_i$): {systematic_risk:.3f}")
        print(f"Calculated Idiosyncratic Risk ($V_i$): {idiosyncratic_risk:.3f}")
        print("\\n") # Add a newline for better spacing in output

        # Plot current risks
        plot_current_risks(systematic_risk, idiosyncratic_risk)

        # Plot risk reduction
        plot_risk_reduction_over_time(systematic_risk, total_time_transition)
    ```

*   **Code Cell Execution**:
    Execute the definition of `update_risk_dashboard`.

*   **Markdown Cell**:
    The dashboard update logic is now defined. We can proceed to display the interactive components.

---

### Section 10: Display the Interactive Dashboard

*   **Markdown Cell**:
    Interact with the widgets below to dynamically assess your AI job displacement risk. Change your skill level, educational attainment, industry, and job role to see how these factors influence your systematic ($H_i$) and idiosyncratic ($V_i$) risk scores, as well as your potential for risk reduction through career diversification.

*   **Code Cell**:
    This cell should instantiate widgets and display the interactive output:
    ```
    skill_w, education_w, industry_w, job_role_w = create_risk_input_widgets()

    # Arrange widgets in a cleaner layout
    input_widgets = VBox([
        skill_w,
        education_w,
        industry_w,
        job_role_w
    ])

    # Display the interactive dashboard
    interactive_dashboard = interact(
        update_risk_dashboard,
        skill=skill_w,
        education=education_w,
        industry=industry_w,
        job_role=job_role_w
    )

    display(input_widgets)
    display(interactive_dashboard)
    ```

*   **Code Cell Execution**:
    Execute the display of the interactive dashboard.

*   **Markdown Cell**:
    The interactive dashboard is now active. Experiment with different inputs to observe the dynamic changes in your risk profile and the potential for mitigation. This interactive exploration demonstrates how different features influence the risk metrics.

---

### Section 11: Understanding Personal Actions and Risk Mitigation

*   **Markdown Cell**:
    The interactive dashboard vividly demonstrates that your personal attributes and career choices significantly impact your risk profile. This aligns with fundamental principles of risk management, where understanding and controlling variables can lead to better outcomes.

    *   **Upskilling (Skill Level & Education)**: Increasing your skill level or pursuing higher education generally leads to lower systematic and idiosyncratic risks. AI tends to automate routine tasks, making specialized, creative, and human-centric skills more valuable.
    *   **Career Path Diversification (Industry & Job Role)**: Strategically transitioning to industries or job roles with lower susceptibility to AI automation (e.g., from 'Routine Task Specialist' to 'Creative Professional') can significantly reduce your systematic risk over time, as shown in the "Projected Risk Reduction" plot. This transition requires proactive planning and continuous learning.
    *   **Proactive Management**: The ability to dynamically assess risk allows for proactive career planning, aligning with the principles of risk management [3].

---

### Section 12: Conclusion

*   **Markdown Cell**:
    This notebook has provided an interactive application to explore the multifaceted nature of AI-driven job displacement risk. By simulating how individual choices regarding skills, education, industry, and job role influence systematic and idiosyncratic risks, we can gain a clearer understanding of potential vulnerabilities and, more importantly, actionable mitigation strategies.

    Remember, while AI presents challenges, it also creates new opportunities. Proactive learning, skill development, and strategic career diversification are powerful tools for navigating the evolving future of work. Understanding your risk profile is the first step towards building a resilient career in an AI-powered world.

