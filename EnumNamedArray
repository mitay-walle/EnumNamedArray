// based on answer by idbrii from https://answers.unity.com/questions/225089/making-a-user-friendly-array-with-indices-based-on.html

using UnityEngine;
#if UNITY_EDITOR
using System;
using UnityEditor;

#endif

public class EnumNamedArrayAttribute : PropertyAttribute
{
    public Type TargetEnum;

    public EnumNamedArrayAttribute(Type TargetEnum)
    {
        this.TargetEnum = TargetEnum;
    }
}
#if UNITY_EDITOR
[CustomPropertyDrawer(typeof(EnumNamedArrayAttribute))]
public class NamedArrayDrawer : PropertyDrawer
{
    public override float GetPropertyHeight(SerializedProperty property, GUIContent label)
    {
        return EditorGUI.GetPropertyHeight(property, label, property.isExpanded);
    }

    public override void OnGUI(Rect position, SerializedProperty property, GUIContent label)
    {
        try
        {
            var config = attribute as EnumNamedArrayAttribute;
            var enum_names = Enum.GetNames(config.TargetEnum);
            int pos = int.Parse(property.propertyPath.Split('[', ']')[1]);
            var enum_label = enum_names.GetValue(pos) as string;
            enum_label = ObjectNames.NicifyVariableName(enum_label.ToLower());
            label = new GUIContent(enum_label);
        }
        catch
        {
        }

        EditorGUI.PropertyField(position, property, label, property.isExpanded);
    }
}
#endif
