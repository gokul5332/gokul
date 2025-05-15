# ----------------------------
# Module: Diagnosis Knowledge Base
# ----------------------------

diagnosis_data = {
    "fever": ["Flu", "COVID-19", "Malaria"],
    "cough": ["Bronchitis", "Flu", "COVID-19"],
    "fatigue": ["Anemia", "Hypothyroidism", "Depression"],
    "headache": ["Migraine", "Tension Headache", "Dehydration"],
    "nausea": ["Food Poisoning", "Gastritis", "Pregnancy"],
    "rash": ["Allergy", "Measles", "Chickenpox"]
}

treatment_data = {
    "Flu": ["Rest", "Hydration", "Paracetamol"],
    "COVID-19": ["Isolation", "Hydration", "Medical attention if severe"],
    "Malaria": ["Antimalarial drugs", "Hospitalization if needed"],
    "Bronchitis": ["Cough syrup", "Inhalation therapy", "Rest"],
    "Anemia": ["Iron supplements", "Dietary changes"],
    "Hypothyroidism": ["Thyroid hormone replacement", "Regular monitoring"],
    "Depression": ["Therapy", "Antidepressants", "Lifestyle changes"],
    "Migraine": ["Painkillers", "Caffeine", "Rest"],
    "Tension Headache": ["Massage", "Pain relievers", "Stress management"],
    "Dehydration": ["Fluids", "Electrolytes", "IV fluids (if severe)"],
    "Food Poisoning": ["Oral rehydration", "Rest", "Bland food"],
    "Gastritis": ["Antacids", "Avoid spicy foods", "Small meals"],
    "Pregnancy": ["Prenatal vitamins", "Rest", "Medical checkups"],
    "Allergy": ["Antihistamines", "Avoid allergen", "Corticosteroids"],
    "Measles": ["Supportive care", "Vitamin A", "Fluids"],
    "Chickenpox": ["Antivirals", "Itch relief creams", "Rest"]
}

# ----------------------------
# Function Definitions
# ----------------------------

def get_symptoms():
    print("\nEnter symptoms separated by commas (e.g., fever, fatigue, headache):")
    raw_input = input(">> ").lower()
    return [s.strip() for s in raw_input.split(",") if s.strip()]

def diagnose(symptoms):
    condition_scores = {}
    for symptom in symptoms:
        conditions = diagnosis_data.get(symptom, [])
        for condition in conditions:
            condition_scores[condition] = condition_scores.get(condition, 0) + 1
    return sorted(condition_scores.items(), key=lambda x: x[1], reverse=True)

def suggest_treatment(diagnoses):
    print("\n🩺 Diagnosis & Treatment Plan:")
    for condition, score in diagnoses[:3]:  # Show top 3 conditions
        print(f"\n🔎 Possible Condition: {condition}")
        treatments = treatment_data.get(condition, ["Consult a medical professional"])
        print("💊 Recommended Treatment:")
        for t in treatments:
            print(f" - {t}")

# ----------------------------
# Main Execution
# ----------------------------

def main():
    print("=== AI Healthcare Diagnostics & Treatment Assistant ===")
    symptoms = get_symptoms()

    if not symptoms:
        print("⚠  No symptoms entered. Please try again.")
        return

    diagnoses = diagnose(symptoms)
    if diagnoses:
        suggest_treatment(diagnoses)
    else:
        print("❗ No matching conditions found. Please consult a healthcare provider.")

if _name_ == "_main_":
    main()
