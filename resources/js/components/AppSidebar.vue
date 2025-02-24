<script setup lang="ts">
import NavFooter from '@/components/NavFooter.vue';
import NavMain from '@/components/NavMain.vue';
import NavUser from '@/components/NavUser.vue';
import { Sidebar, SidebarContent, SidebarFooter, SidebarHeader, SidebarMenu, SidebarMenuButton, SidebarMenuItem } from '@/components/ui/sidebar';
import { type NavItem } from '@/types';
import { Link } from '@inertiajs/vue3';
import { BookOpen, Folder, LayoutGrid, Activity, File, Users, UserCheck, School, Calendar, Award, ClipboardList, Mail, BarChart2, LifeBuoy, Settings, LogOut } from 'lucide-vue-next';
import AppLogo from './AppLogo.vue';

// Define main navigation items with nested children
const mainNavItems: NavItem[] = [
    {
        title: 'Dashboard',
        href: '/dashboard',
        icon: LayoutGrid,
    },
    {
        title: 'Attendance',
        href: '/attendance',
        icon: Activity,
    },
    {
        title: 'Students',
        href: '#', // Use '#' or a fallback URL for parent items
        icon: Users,
        children: [
            {
                title: 'All Students',
                href: '/students',
            },
            {
                title: 'Add Student',
                href: '/students/add',
            },
            {
                title: 'Student Reports',
                href: '/students/reports',
            },
        ],
        isOpen: false, // Initialize isOpen for expand/collapse
    },
    {
        title: 'Teachers',
        href: '#', // Use '#' or a fallback URL for parent items
        icon: UserCheck,
        children: [
            {
                title: 'All Teachers',
                href: '/teachers',
            },
            {
                title: 'Add Teacher',
                href: '/teachers/add',
            },
            {
                title: 'Teacher Schedules',
                href: '/teachers/schedules',
            },
        ],
        isOpen: false, // Initialize isOpen for expand/collapse
    },
    {
        title: 'Classes',
        href: '#', // Use '#' or a fallback URL for parent items
        icon: School,
        children: [
            {
                title: 'All Classes',
                href: '/classes',
            },
            {
                title: 'Add Class',
                href: '/classes/add',
            },
            {
                title: 'Class Timetable',
                href: '/classes/timetable',
            },
        ],
        isOpen: false, // Initialize isOpen for expand/collapse
    },
    {
        title: 'Grades',
        href: '#', // Use '#' or a fallback URL for parent items
        icon: Award,
        children: [
            {
                title: 'All Grades',
                href: '/grades',
            },
            {
                title: 'Grade Reports',
                href: '/grades/reports',
            },
        ],
        isOpen: false, // Initialize isOpen for expand/collapse
    },
    {
        title: 'Exams',
        href: '#', // Use '#' or a fallback URL for parent items
        icon: ClipboardList,
        children: [
            {
                title: 'All Exams',
                href: '/exams',
            },
            {
                title: 'Add Exam',
                href: '/exams/add',
            },
            {
                title: 'Exam Results',
                href: '/exams/results',
            },
        ],
        isOpen: false, // Initialize isOpen for expand/collapse
    },
    {
        title: 'Assignments',
        href: '#', // Use '#' or a fallback URL for parent items
        icon: BookOpen,
        children: [
            {
                title: 'All Assignments',
                href: '/assignments',
            },
            {
                title: 'Add Assignment',
                href: '/assignments/add',
            },
            {
                title: 'Assignment Submissions',
                href: '/assignments/submissions',
            },
        ],
        isOpen: false, // Initialize isOpen for expand/collapse
    },
    {
        title: 'Messages',
        href: '/messages',
        icon: Mail,
    },
    {
        title: 'Reports',
        href: '#', // Use '#' or a fallback URL for parent items
        icon: BarChart2,
        children: [
            {
                title: 'Attendance Reports',
                href: '/reports/attendance',
            },
            {
                title: 'Grade Reports',
                href: '/reports/grades',
            },
            {
                title: 'Exam Reports',
                href: '/reports/exams',
            },
        ],
        isOpen: false, // Initialize isOpen for expand/collapse
    },
];

// Define footer navigation items
const footerNavItems: NavItem[] = [
    {
        title: 'Natania',
        href: 'http://localhost:8080',
        icon: BookOpen,
    },
    {
        title: 'Joy',
        href: 'http://localhost:8080',
        icon: BookOpen,
    },
    {
        title: 'Github Repo',
        href: 'https://github.com/laravel/vue-starter-kit',
        icon: Folder,
    },
    {
        title: 'Documentation',
        href: 'https://laravel.com/docs/starter-kits',
        icon: BookOpen,
    },
    {
        title: 'Support',
        href: '/support',
        icon: LifeBuoy,
    },
    {
        title: 'Settings',
        href: '/settings',
        icon: Settings,
    },
    {
        title: 'Logout',
        href: '/logout',
        icon: LogOut,
    },
];
</script>

<template>
    <Sidebar collapsible="icon" variant="inset">
        <SidebarHeader>
            <SidebarMenu>
                <SidebarMenuItem>
                    <SidebarMenuButton size="lg" as-child>
                        <Link :href="route('dashboard')">
                            <AppLogo />
                        </Link>
                    </SidebarMenuButton>
                </SidebarMenuItem>
            </SidebarMenu>
        </SidebarHeader>

        <SidebarContent>
            <NavMain :items="mainNavItems" /> <!-- Pass mainNavItems to NavMain -->
        </SidebarContent>

        <SidebarFooter>
            <NavFooter :items="footerNavItems" />
            <NavUser />
        </SidebarFooter>
    </Sidebar>
    <slot />
</template>
