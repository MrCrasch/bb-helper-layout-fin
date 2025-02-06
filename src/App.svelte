<script>
	import List from "./List.svelte";
	import { onMount } from "svelte";

	let layout = []; // Panels with components
	let trash = []; // Store deleted components

	const data = {
		InsertCountAfterPanel: 1,
		Panels: [
			{
				PanelName: "",
				NumberOfColumns: 3,
				Components: [
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Evaluator, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Maths Evaluator",
						Alias: "Maths Eval",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Printer, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Printer",
						Alias: "Printer",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Inputs.ConstantInput, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Constant",
						Alias: "Constant",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Differencer, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Differencer",
						Alias: "Differencer",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Pid, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "PID Controller",
						Alias: "PID",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.GenericBlockSetter, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Generic block setter",
						Alias: "GBS",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Ai.AiTargetInfo, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Primary target info",
						Alias: "PTI",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.AltitudeInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Altitude",
						Alias: "Altitude",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Inputs.RandomInput, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Random number",
						Alias: "Random",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.PositionInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Position",
						Alias: "Position",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.OrientationInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Orientation input",
						Alias: "Orientation",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.SpeedInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Speed",
						Alias: "Speed",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.TimeInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Time",
						Alias: "Time",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.VariableWriter, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Variable Writer",
						Alias: "Variable Writer",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.VariableReaderInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Variable Reader",
						Alias: "Variable Reader",
					},
				],
			},
			{
				PanelName: "",
				NumberOfColumns: 3,
				Components: [
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Clamp, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Clamp",
						Alias: "Clamp",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Adder, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Sum",
						Alias: "Sum",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Multiply, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Multiply",
						Alias: "Multiply",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.LogicGate, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Logic Gate",
						Alias: "Logic Gate",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.MaxMin, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Max/Min",
						Alias: "Max/Min",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Sorter, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Sorter",
						Alias: "Sorter",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.ComplexControlInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Complex Control",
						Alias: "Complex",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.ControlInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Propulsion",
						Alias: "Propulsion In",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.PropulsionModule, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Propulsion",
						Alias: "Out Propulsion",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.RotationInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Rotation",
						Alias: "Rotation",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.CustomPropulsionInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Custom propulsion input",
						Alias: "CustomAxis In",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.CustomPropulsionSetter, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Custom propulsion",
						Alias: "Out CustomAxis",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.StabilityInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Stability",
						Alias: "Stability",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.GenericGetter.GenericBlockGetter, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Generic block getter",
						Alias: "GBG",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.EventInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Event input",
						Alias: "Event input",
					},
				],
			},
			{
				PanelName: "",
				NumberOfColumns: 3,
				Components: [
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Switch, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Switch",
						Alias: "Switch",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Inputs.Comment, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Comment",
						Alias: "Comment",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Accumulator, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Accumulator (with threshold)",
						Alias: "Accumulator",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.FuzzyThreshold, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Threshold",
						Alias: "Threshold",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.OneShot, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "One shot",
						Alias: "One shot",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.DriveModule, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Drives",
						Alias: "Drives",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Delay, Breadboards, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Delay Pulse",
						Alias: "Delay Pulse",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.TimeOfDayInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Time of Day info",
						Alias: "Time of Day",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.FlagshipInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Flagship info",
						Alias: "Flagship info",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Ai.AiBehaviourSelect, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Behaviour selector",
						Alias: "Behaviour",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Ai.AiManoeuvreSelect, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Manoeuvre selector",
						Alias: "Manoeuvre",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Ai.AiSteeringpointInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Steering point info",
						Alias: "Steering",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.AIBehaviourInput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "AI Behaviour Input",
						Alias: "AI Behaviour",
					},
					{
						QualifiedName:
							"BrilliantSkies.Common.Circuits.ComponentTypes.Inputs.AIManoeuvreOutput, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "AI Manoeuvre Output",
						Alias: "AI Manoeuvre",
					},
				],
			},
			{
				PanelName: "",
				NumberOfColumns: 3,
				Components: [
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Playback, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Playback",
						Alias: "Playback",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.AnimatorControl, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Anim. control",
						Alias: "Anim.Control",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.AnimatorBulkPosition, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Anim. position",
						Alias: "Anim.Position",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Animator.IkPositionControl, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Anim. Ik position",
						Alias: "Ik position",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Animator.IkRotationControl, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Anim. IK rotation",
						Alias: "IK rotation",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Animator.BodyPositionControl, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Anim. body look",
						Alias: "A.body look",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Animator.AnimatorLinkEditor, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "Anim. LINK edit",
						Alias: "A.LINK edit",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Animator.LinkSource, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "LINK subobject",
						Alias: "LINK subobj",
					},
					{
						QualifiedName:
							"BrilliantSkies.Blocks.BreadBoards.Animator.LinkDestination, Ftd, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null",
						DefaultName: "LINK limb",
						Alias: "LINK limb",
					},
				],
			},
		],
	};
	
	layout = data.Panels || []; // Ensure layout is an array

	// Assign unique IDs properly
	layout = layout.map((panel, index) => ({
		...panel,
		id: index + 1, // Unique Panel ID
		Components: panel.Components.map((component, i) => ({
			...component,
			id: `${index + 1}-${i + 1}`, // Unique Component ID per panel
		})),
	}));


	function addPanel(index) {
		const newPanel = {
			id: layout.length + 1,
			PanelName: `New Panel ${layout.length + 1}`,
			NumberOfColumns: 3,
			Components: [],
		};

		layout = [
			...layout.slice(0, index + 1),
			newPanel,
			...layout.slice(index + 1),
		];
		//console.log('Updated layout after addition:', layout);
	}

	function deletePanel(index) {
		if (layout.length > 1) {
			const panelToDelete = layout[index];

			trash = [
				...trash,
				...panelToDelete.Components.map((comp) => ({
					...comp,
					id: `trash-${panelToDelete.id}-${comp.id}`,
				})),
			];

			layout = [...layout.slice(0, index), ...layout.slice(index + 1)];
			//console.log('Updated layout:', layout);
			//console.log('Updated trash:', trash);
		} else {
			console.log("Cannot delete the last panel");
		}
	}

	function handleUpdateAlias(event) {
		const { id, newAlias } = event.detail;

		layout = layout.map((panel) => ({
			...panel,
			Components: panel.Components.map((comp) =>
				comp.id === id ? { ...comp, Alias: newAlias } : comp,
			),
		}));

		//console.log('Updated layout:', layout);
	}

	function handleUpdateCol(event) {
		const { col, panelId } = event.detail;

		layout = layout.map((panel) =>
			panel.id === panelId ? { ...panel, NumberOfColumns: col } : panel,
		);

		//console.log('Updated panel columns:', layout);
	}

	function handleUpdateSort(event, panelId) {
		layout = layout.map((panel) =>
			panel.id === panelId
				? { ...panel, Components: event.detail.sortedItems }
				: panel,
		);
	}

	function downloadLayout() {
		// Create a deep copy of layout without modifying the original
		let cleanedPanels = layout.map((panel) => ({
			...panel,
			id: undefined, // Remove panel ID
			Components: panel.Components.map((component) => ({
				...component,
				id: undefined, // Remove component ID
			})),
		}));

		// Structure JSON correctly with InsertCountAfterPanel at the top level
		let layoutWithoutIds = {
			InsertCountAfterPanel: 1, // Preserve this field
			Panels: cleanedPanels,
		};

		// Remove undefined keys
		layoutWithoutIds = JSON.parse(JSON.stringify(layoutWithoutIds));

		const json = JSON.stringify(layoutWithoutIds, null, 2);
		const blob = new Blob([json], { type: "application/txt" });
		const url = URL.createObjectURL(blob);

		const a = document.createElement("a");
		a.href = url;
		a.download = "layout.txt";
		document.body.appendChild(a);
		a.click();
		document.body.removeChild(a);
		URL.revokeObjectURL(url);
	}
</script>

<h3>Layout Helper by Crumbs</h3>
<button on:click={downloadLayout}>Download JSON</button>
<hr />

{#each layout as panel, index}
	<div>
		<h4>{panel.PanelName}</h4>

		<List
			items={panel.Components}
			nCol={panel.NumberOfColumns}
			on:updateAlias={handleUpdateAlias}
			on:updateCol={(e) =>
				handleUpdateCol({ ...e.detail, panelId: panel.id })}
			on:updateSort={(e) => handleUpdateSort(e, panel.id)}
		/>

		<button on:click={() => deletePanel(index)}>Delete this Panel</button>
		<button on:click={() => addPanel(index)}>Add Panel here</button>
		<hr />
	</div>
{/each}

<hr />
<h4>Removed Items:</h4>
<List items={trash} nCol={3} />
