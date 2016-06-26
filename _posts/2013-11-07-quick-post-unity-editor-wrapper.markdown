---
layout: post
title:  "Quick post: Unity editor wrapper"
date:   2013-11-07 21:11:00 +0100
categories: updates gamedev Unity3D
---
I've seen people reverse engineer the transform editor or doing their own thing.
In Unity 4 you can render the original editor inside yours as long as you have
the original editors type.  
Here's an example for a transform editor wrapper, but you can wrap anything you
want, like a MeshRenderer or a TextureImporter (haven't tried yet).  
You may want to wrap other Editor methods besides OnInspectorGUI as well.

{% highlight csharp linenos %}
using UnityEngine;
using UnityEditor;

[CustomEditor(typeof(Transform))]
public class TransformEditorWrapper : Editor {
	Editor transformEditor;
	
	void OnEnable() {
		Transform transform = target as Transform;
		System.Type t = typeof(UnityEditor.EditorApplication).Assembly.GetType("UnityEditor.TransformInspector");
		transformEditor = Editor.CreateEditor(transform, t);
	}
	
	public override void OnInspectorGUI() {
		GUI.changed = false;
		transformEditor.OnInspectorGUI();

		Transform transform = target as Transform;
		GUILayout.Label("WRAPPED!");
		// do your stuff here...
	}
	
	void OnDisable() {
		DestroyImmediate(transformEditor);
	}
}
{% endhighlight %}